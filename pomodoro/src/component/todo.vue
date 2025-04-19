<script setup lang="ts">
import { ref } from 'vue'

interface Task {
  id: number
  text: string
  completed: boolean
}

const newTask = ref('')
const tasks = ref<Task[]>([])

const toggleTask = (index: number) => {
  tasks.value[index].completed = !tasks.value[index].completed
}

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

const removeTask = (index: number) => {
  tasks.value.splice(index, 1)
}
</script>

<template>
  <div>
    <h1 class="text-2xl font-bold text-center">Todo List</h1>

    <!-- input -->
    <div>
      <input v-model="newTask" type="test" placeholder="New Todo ?">
      <button @click="addTask">
        Add
      </button>
    </div>
    
    
    <div>
      <li v-for="(task,index) in tasks" :key="task.id">

        <span @click="toggleTask(index)">{{ task.text }}</span>
        <button @click="removeTask(index)">X</button>

      </li>
    </div>
  </div>
</template>
