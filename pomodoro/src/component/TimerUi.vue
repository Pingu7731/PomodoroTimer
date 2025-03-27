<script setup>

import { ref } from "vue";
const focusTime = ref(25);
const restTime = ref(5);
const currentTime = ref(0);
const isFocus = ref(true);
let interval = null;

const start = () => {
    if (interval) return; //no multiple intervals

    currentTime.value = (isFocus.value ? focusTime.value : restTime.value) * 60;
    // if its focus, show focus time else show resttime
    interval = setInterval(() => {
        if (currentTime.value > 0) {
            currentTime.value--;
        } else {
            clearInterval(interval);
            interval = null;
            isFocus.value = !isFocus.value; //switch mode
            start(); //start sess
        }
    }, 1000); //1000= run every 1000ms
};
const pause = () => {
    clearInterval(interval);
    interval = null;
};

const reset = () => {
    pause();
    isFocus.value = true;
    currentTime.value = focusTime.value * 60;

    //if reset change back to focus time
};

const formatTime = (seconds) => {
    const mins = Math.floor(seconds / 60);
    const secs = seconds % 60;
    return `${String(mins).padStart(2, "0")} : ${String(secs).padStart(2, "0")}`;
    //formatting the string to having 0 at the start of the string when number is 1 digit
    //padstart(2,"" )means two digit
};
</script>

<template>
    <main>
        <div class="timeDivContainer">
            <div class="timeRow">
                <label>Focus Time (minutes) : </label>
                <input type="number" v-model="focusTime" min="1" />
            </div>
            <div class="timeRow">
                <label>Rest Time (minutes) : </label>
                <input type="number" v-model="restTime" min="1" />
            </div>
        </div>
        <h2>{{ isFocus ? "Focus Time" : "Rest Time" }}</h2>
        <div class="timer">{{ formatTime(currentTime) }}</div>
        <div class="buttons">
            <button @click="start">Start</button>
            <button @click="pause">Pause</button>
            <button @click="reset">Reset</button>
        </div>
    </main>
</template>

<style scoped>
main {
    text-align: center;
    font-family: sans-serif;
    margin: auto;
    padding: 20px;
    color: #ffffff;
}

h2 {
    font-size: 2rem;
    margin-bottom: 10px;
}

.timeDivContainer {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 30px; 
    padding: 15px;
    
}

.timeRow {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5px; 
}
.timerRow label{
    font-size: 5rem;
    font-weight: 500;
    font-family: "Poppins",sans-serif;
    color: aliceblue;
    letter-spacing: 1px ;
}
.timeRow input{
  width: 70px;
  text-align: center;
  font-size: 2rem;
  padding: 8px;
  border: 1px solid #141414;
  background: #383838;
  color: white;
  border-radius: 6px;
  outline: none;
  transition: 0.4s;
}
.timeRow input:focus{
    border-color: #ababab;
    box-shadow: 0 0 10px #414141;
}

.timer {
    font-size: 3rem;
    font-weight: bold;
    margin: 20px 0;
    text-shadow: 0 0 10px rgb(214, 214, 214),0 0 20px rgb(214, 214, 214) ;
}
input {
    width: 55px;
    text-align: center;
    margin: 5px;
}
.buttons {
    display: flex;
    justify-content: center;
    gap: 50px;
}
button {
    padding: 10px 16px;
    font-size: 1rem;
    background: #414141;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.3s ease, transform 0.2s;
    box-shadow: 0 4px 6px rgba(17, 17, 17, 0.4);
}
button:hover {
    background: #414141;
    transform: scale(1.05);
}
button:active {
    background: rgb(4, 4, 4);
    transform: scale(0.95);
}

</style>