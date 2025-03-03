<script setup>
import TimerUi from "./component/TimerUi.vue";
import toggleDark from "./component/toggleDark.vue";
</script>

<template>
  <main>
    <h1>Pomodoro Timer</h1>
    <TimerUi />
    <!-- <toggleDark /> -->
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
</style>
