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

const calculate = () => {
  try {
    display.value = eval(display.value).toString();
  } catch (error) {
    display.value = "Error";
  }
};


//Computed Property For Dynamic class binding//

const displayClass = computed(() => {
  return display.value.length > 12 ? "small-text" : '';
})


const clearDisplay = () => {
  return display.value = "0"
}




</script>




<template>
  <div>
    <div class="calculator">
      <input v-model="display" :class="displayClass"  readonly/>
     <br> <br><button @click="appendToDisplay('7')">7</button>
      <button @click="appendToDisplay('8')">8</button>
      <button @click="appendToDisplay('9')">9</button>
      <button @click="appendToDisplay('/')">/</button><br>

       <button @click="appendToDisplay('4')">4</button>
      <button @click="appendToDisplay('5')">5</button>
      <button @click="appendToDisplay('6')">6</button>
      <button @click="appendToDisplay('*')">*</button><br>

       <button @click="appendToDisplay('1')">1</button>
      <button @click="appendToDisplay('2')">2</button>
      <button @click="appendToDisplay('3')">3</button>
      <button @click="appendToDisplay('-')">-</button><br>

      <button @click="appendToDisplay('0')">0</button>
      <button @click="appendToDisplay('.')">.</button>
      <button @click="calculate()">=</button>
      <button @click="appendToDisplay('+')">+</button>
    </div>

    <br><button @click="clearDisplay">Clear</button>

  </div>
</template>
