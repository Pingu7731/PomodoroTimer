<script lang="ts" setup>
import TimerUi from "./component/TimerUi.vue";
import Todo from "./component/todo.vue";
import ToggleDark from "./component/toggleDark.vue";
</script>

<template>
  <div class="animate-ping">
  <div class="animate-spin">
      <div class="animate-bounce">
      <ToggleDark />
      <main>
        <h1>Pomodoro Timer</h1>
        <TimerUi />
        <Todo/>
      </main>
    </div>
  </div>
  </div>
</template>

<style>
main {
  flex-direction: column;
  text-align: center;
}
</style>
