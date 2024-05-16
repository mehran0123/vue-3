<script setup>
import { ref } from 'vue';

const userName = ref('');
const userProfile = ref('');
const error = ref(null);



const getUserProfile = async () => {
    try {
        const response = await fetch(`http://api.github.com/users/${userName.value}`)
        const data = await response.json();
        console.log('data ===>',data);
        if (response.ok) {
            userProfile.value = data;
            error.value = null;
        } else {
            userProfile.value = null;
            error.value = `Error: ${data.message}`
        }
    }catch(error){
        console.log('Error fetching data:', error);
        error.value = 'an error occure while fetching data.'
    }
}
 
</script>

<template>
    <h1>Github Profile</h1>
    <div>
        <input v-model="userName" placeholder="Enter github username" @input="getUserProfile" />
    </div>
    <hr>
    <div v-if="userProfile">
      <h2>User Details</h2>
      <hr>
      <p><strong>Name:</strong>{{ userProfile.login }}</p>
      <p><strong>Location:</strong>{{ userProfile.location }}</p>
      <p><strong>Followers:</strong>{{ userProfile.followers }}</p>
      <p><strong>Following:</strong>{{ userProfile.following }}</p>
      <p><strong>Public Repos:</strong>{{ userProfile.public_repos }}</p>
      <hr>  
    <img :src="userProfile.avatar_url" :alt="userName.login" />
    </div>
    <div v-if="error">
    <h4>{{ error }}</h4>
    </div>

</template>