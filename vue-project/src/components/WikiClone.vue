<script setup>
import { ref } from 'vue';
const searchQury = ref('');
const searchResult = ref([]);
const isLoading = ref(false);
const error = ref(null);
const isDarkTheme = ref();

const searchWikiPedia = async (query) => {

    const encodedQuery = encodeURIComponent(query)
    const endpoint = `https://en.wikipedia.org/w/api.php?action=query&list=search&prop=info&inprop=url&utf8=&format=json&origin=*&srlimit=10&srsearch=${encodedQuery}`


    try {
        isLoading.value = true;

        const res = await fetch(endpoint)
        const data = await res.json();


        if (data.query && data.query.search) {
            searchResult.value = data.query.search
            error.value = null;
        } else {
            searchResult.value = []; 
            error.value = 'No result found';
        }
        
    } catch (err) {
        console.error('Error fethcing data:', err);
        searchResult.value = [];
        error.value = 'An Error occured while fetching data'
    } finally {
         isLoading.value = false;
    }
}



const toggleTheme = () => {
    isDarkTheme.value = !isDarkTheme.value
}


const submitSearch = () => {
    if (searchQury.value.trim() !='') {
        searchWikiPedia(searchQury.value);
    } else {
        searchResult.value = [];
        error.value = 'Please enter a valid search term.'
    }
}

</script>


<template>
    <div :class="{'dark-theme' : isDarkTheme}">
        <div class="container">
            <div class="header-container">
                <h1>Search Wikipedia</h1>
                <span id="theme-toggler" @click="toggleTheme">{{ isDarkTheme ? 'Light' : 'Dark' }}</span>
            </div>
            <form @submit.prevent="submitSearch">
                
                <input type="text" v-model="searchQury" placeholder="Enter Search term" />
                <button type="submit">Search</button>
            </form>

            <div id="search-result">
                <div v-if="isLoading">Loading...</div>
                <p v-if="searchResult.length">
                    <div v-for="(result,index) in searchResult" :key="index">
                        <h3>
                            <a :href="`https://en.wikipedia.org/?curid=${result.pageid}`" target="_blank" rel="noopener">{{ result.title }}</a>
                        </h3>
                         <a :href="`https://en.wikipedia.org/?curid=${result.pageid}`" target="_blank" rel="noopener">{{ `https://en.wikipedia.org/?curid=${result.pageid}` }}</a>
                    
                        <p v-html="result.snippet"></p>
                    
                        </div>
                </p>
            </div>
        </div>
    </div>

</template>