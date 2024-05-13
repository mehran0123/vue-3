<script setup>
import { ref, computed } from "vue";

const formData = ref({
    name: "",
    email: "",
    password: ""
});

const isNameValid = computed(() => formData.value.name.trim() != '')
const isEmailValid = computed(() => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.value.email))
const isPassword = computed(() => formData.value.password.length >= 8)
const isFormvalid = computed(() => isNameValid.value && isEmailValid.value && isPassword.value)

const submitForm = () => {
    if (isFormvalid) {
        //Write success code here
         console.log('form Submited...');
    } else {
         console.log("form validation error, please check form values");
    }
}


</script>

<template>
   <div>
    <form @submit.prevent="submitForm">
        <div class="form-group">
            <label for="name">Name:</label>
            <input type="text" v-model="formData.name" id="name"/>
            <span v-if="!isNameValid">Name is required</span>
        </div>
        <div class="form-group">
            <label for="email">Email:</label>
            <input type="text" v-model="formData.email" id="email"/>
            <span v-if="!isEmailValid">Email is required</span>
        </div>
        <div class="form-group">
            <label for="password">Password:</label>
            <input type="text" v-model="formData.password" id="password"/>
            <span v-if="!isPassword">Password is required</span>
        </div>
    </form>
    <button type="submit" @click="submitForm" :disabled="!isFormvalid">Submit</button>
   </div>
</template>