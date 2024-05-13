<script setup>

import { ref } from "vue";
const items = ref([
  {
    title: "Qoute 1",
    content: "Mehran-1",
    open:false
  },
  {
    title: "Qoute 2",
    content: "Mehran 2",
    open:false
  },
  {
    title: "Qoute 3",
    content: "Mehran 3",
    open:true
  },
  {
    title: "Qoute 4",
    content: "Mehran 4",
    open:false
  },
  {
    title: "Qoute 5",
    content: "Mehran 5",
    open:false
    },
]);
    const  toggleAccordion = (index) => {
        items.value = items.value.map((item, i) => ({
            ...item, 
            open:i === index ? !item.open : false
        }))
    }

    

</script>
<template>
 <div class="accordian-container">
    <div v-for="(item,index) in items" :key="index" class="accordion">
        <div class="accordion-header" @click="toggleAccordion(index)">
        {{ item.title }}
    <span>{{ item.open ? "🔽" : "▶" }}</span>
    </div>
    <div v-show="item.open">
        {{ item.content }}
    </div>
    </div>
 </div>
</template>