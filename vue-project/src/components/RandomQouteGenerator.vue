<script setup>
import { ref, onMounted } from "vue";
const qoutes = ref([
  {
    text: "Qoute 1",
    authot: "Mehran-1",
  },
  {
    text: "Qoute 2",
    authot: "Mehran 2",
  },
  {
    text: "Qoute 3",
    authot: "Mehran 3",
  },
  {
    text: "Qoute 4",
    authot: "Mehran 4",
  },
  {
    text: "Qoute 5",
    authot: "Mehran 5",
  },
]);

const currentQoute = ref({ text: "", authot: "" });

const getRandonQoute = () => {
  const randomIndex = Math.floor(Math.random() * qoutes.value.length);
  currentQoute.value = qoutes.value[randomIndex];
};

onMounted(() => {
  getRandonQoute
});
</script>

<template>
  <div class="qoute-generator">
    <h1 class="app-title">Random Qoute Generator</h1>
    <blockquote>
      <p>{{ currentQoute.text }}</p>
      <cite>{{ currentQoute.authot }}</cite>
    </blockquote>

    <button @click="getRandonQoute">Get Random Qoute</button>
  </div>
</template>
