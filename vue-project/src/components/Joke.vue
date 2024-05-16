<script setup>
import { ref } from 'vue';
import axios from 'axios';

const jokes = ref(null);

const fetchJokes = async () => {
    try {
        const res = await axios.get('http://icanhazdadjoke.com/', {
            headers:{Accept:'application/json'}
        })
        jokes.value = res.data.joke;
    } catch (error) {
        console.log('Error fetching:',error);
    }
}


</script>


<template>
    <h1>I can has jokes API Project</h1>
    <div>
        <h2>Jokes</h2>
        <button @click="fetchJokes">Get Jokes</button>
        <br/><br/>
        <hr>
        <div v-if="jokes">{{ jokes }}</div>
    </div>
</template>