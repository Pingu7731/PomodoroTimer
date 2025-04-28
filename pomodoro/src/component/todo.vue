<script setup lang="ts">
import { onMounted, ref,watch } from 'vue'

interface Task {
  id: number
  text: string
  completed: boolean
}

const newTask = ref('')
const tasks = ref<Task[]>([])
const editingIndex= ref<number |null>(null)
const editingText= ref('')


const toggleTask = (index: number) => {
  tasks.value[index].completed = !tasks.value[index].completed
}
//save local strage , prevent ur data gone gone

const TASKS_KEY = 'todo-tasks'
onMounted(() => {
  const saved = localStorage.getItem(TASKS_KEY)
  if(saved)
  {
  tasks.value = JSON.parse(saved)
  }
})
watch(tasks, (val) => {
  localStorage.setItem(TASKS_KEY,JSON.stringify(val))
},{deep:true})

const addTask = () => {
  const text = newTask.value.trim()
  if (text) {
    tasks.value.push({
      id: Date.now(),
      text,
      completed: false,
    })
    newTask.value = ''
  }
}

const startEdit =(index:number)=>{
   editingIndex.value=index
   editingText.value=tasks.value[index].text
}
const saveEdit=(index : number) => {
  const text= editingText.value.trim()
  if(text){
    tasks.value[index].text = text
    editingIndex.value=null
    editingText.value=''
  }
} 
const cancelEdit=()=>{
  editingText.value=''
  editingIndex.value=null
}

const removeTask = (index: number) => {
  tasks.value.splice(index, 1)
}

</script>

<template>
 
  <div class=" flex items-center justify-center" > 
    <div class="w-full max-w-d p6 rounded-xl shadlow-lg spacy-y-4"> 
      <h1 class="text-2xl font-bold text-center">Todo List</h1>
      <!-- input -->
      <div class="flex gap-2">
        <input v-model="newTask" type="test" placeholder="New Todo ?"
        class=" flex-1 px-3 py-2 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-400"
        >
        <button @click="addTask"
        class="font-semibold px-4 py-2"
        >
          Add
        </button>
      </div>
    
    
      <div class="max-h-60 overflow-auto pr-1 hide-scrollbar">
      
        <transition-group name="fade"tag="ul" class="space-y-1.5">
          <li v-for="(task,index) in tasks" :key="task.id"
          class="flex items-center justify-between  rounded-md transition-all gap-y-1"
           >
            <span v-if="editingIndex !==index"
            @click="toggleTask(index)"
            :class="{
            'line-through text-blue-400': task.completed,'cursor-pointer':true
            }"
            >
           
            {{ task.text }}
          
          </span>
          <input v-else v-model="editingText" type="text" 
          class="px-2 py-1 rounded-md boder focus:outline-none" >
            
          <div class="flex gap-2">
              <button v-if="editingIndex === index" @click="saveEdit(index)" class="text-green-500 font-semibold">Save</button>
              <button v-if="editingIndex === index" @click="cancelEdit" class="text-gray-500 font-semibold">Cancel</button>
              <button v-else @click="startEdit(index)" class="text-blue-500 font-semibold">Edit</button>
              <button @click="removeTask(index)" class="text-red-500 font-semibold">X</button>
            </div>
          
          </li>
        </transition-group>
      </div>
    </div>
  </div>
</template>
<style>
.fade-enter-active,
.fade-leave-active{
  transition: all 0.3s ease;
}

.fade-enter-from{
  opacity:0;
  transform: translateY(90px);
}
.fade-leave-to{
  opacity: 0;
  transform: translateY(90px);
}
.hide-scrollbar::-webkit-scrollbar {
  display: none;
}

.hide-scrollbar {
  overflow: scroll; /* Keep scrollable */
  -ms-overflow-style: none;  /* For Internet Explorer 10+ */
  scrollbar-width: none; /* For Firefox */
}
</style>