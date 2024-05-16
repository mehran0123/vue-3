<script setup>
import { ref } from "vue";

const steps = ref(['Step 1', 'Step 2', 'Step 3']);

const currentStep = ref(0);


const nextStep = () => {
    if (currentStep.value < steps.value.length - 1) {
        currentStep.value++;
    }
}


const prevStep = () => {
    if (currentStep.value > 0) {
        currentStep.value--;
    }   
}


</script>

<template>
    <h1>Progress Steps</h1>
    <div class="progress-bar">
        <div v-for="(step,index) in steps" :key="index" :class="{'step-active':index === currentStep}">{{ step }}</div>
        <div>
            <button @click="prevStep" :disabled="currentStep === 0">Previous</button>
            <button @click="nextStep" :disabled="currentStep === steps.length - 1">Next</button>
        </div>
    </div>
</template>