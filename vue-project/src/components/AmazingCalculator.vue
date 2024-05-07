<script setup>
import { ref, computed } from "vue";
const display = ref("0");

const appendToDisplay = (value) => {
  if (display.value === "0" && value != ".") {
    display.value = value;
  } else {
    display.value += value;
  }
};

const calculator = () => {
  try {
    display.value = eval();
  } catch (error) {
    display.value = "Error";
  }
};
</script>
<template>
  <h1>Amazing Calculator</h1>
</template>
