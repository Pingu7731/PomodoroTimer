<script lang="ts" setup>
import TimerUi from "./component/TimerUi.vue";
import Todo from "./component/todo.vue";
import ToggleDark from "./component/toggleDark.vue";
</script>

<template>
  
      <ToggleDark />
      <main>
        <h1>Pomodoro Timer</h1>
        <TimerUi />
        <Todo/>
      </main>
  

</template>

<style>
main {
  flex-direction: column;
  text-align: center;
}
</style>
