<script setup>
import TimerUi from "./component/TimerUi.vue";
import toggleDark from "./component/toggleDark.vue";
</script>

<template>
  <toggleDark />
  <main>
    <h1>Pomodoro Timer</h1>
    <TimerUi />
  </main>
</template>

<style>
main {
  flex-direction: column;
  text-align: center;
}
</style>
