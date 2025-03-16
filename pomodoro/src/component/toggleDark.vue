<script setup>
import { ref, onMounted, watch } from "vue";

const isDarkMode = ref(true);

// load safe time
onMounted(() => {
  isDarkMode.value = localStorage.getItem("theme") === "light";
  updateTheme();
});

// update theme if clic
watch(isDarkMode, (newVal) => {
  localStorage.setItem("theme", newVal ? "light" : "dark");
  updateTheme();
});

const updateTheme = () => {
  if (isDarkMode.value) {
    document.documentElement.classList.add("dark-mode");
  } else {
    document.documentElement.classList.remove("dark-mode");
  }
};
</script>

<template>
  <label class="switch">
    <input type="checkbox" v-model="isDarkMode" />
    <span class="slider"></span>
  </label>
</template>

<style>

/* the containter */
.switch {
  position: relative;
  display: inline-block;
  width: 50px;
  height: 26px;
}

/* hide checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: 0.4s;
  border-radius: 26px;
}

.slider:before {
  content: "";
  position: absolute;
  height: 18px;
  width: 18px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: 0.4s;
  border-radius: 50%;
}

/* when checked */
input:checked + .slider {
  background-color: #444;
}

input:checked + .slider:before {
  transform: translateX(24px);
}

/* Dark mode */
.dark-mode {
  background-color: #222;
  color: white;
}
</style>
