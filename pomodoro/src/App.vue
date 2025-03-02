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
    <h1>Pomodoro Timer</h1>
    <div class="timeDivContainer">
      <div class="timerName">
        <label>Focus Time (minutes) : </label>
        <label>Rest Time(minutes) : </label>
      </div>
      <div class="timerInput">
        <input type="number" v-model="focusTime" min="1" />
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

<style>
* {
  background-color: grey;
  margin: 5px;
}

main {
  text-align: center;
}
h2 {
  font-size: 2rem;
}
.timeDivContainer {
  display: flex;
  align-items: center;
  justify-content: center;
}
.timerName {
  display: flex;
  align-items: center;
  flex-direction: column;
}
.timerInput {
  display: flex;
  align-items: center;
  flex-direction: column;
}
.timer {
  font-size: 3rem;
  margin: 20px 0;
}
input {
  width: 55px;
  text-align: center;
  margin: 5px;
}
</style>
