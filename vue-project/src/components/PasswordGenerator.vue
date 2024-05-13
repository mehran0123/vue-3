 <script setup>
import { ref } from 'vue';
const passwordLenght = ref(12);
const includeUppercase = ref(true)
const includeNumbers = ref(true)
const includeSymbols = ref(true)
const generatedPassword = ref('')

const generatePassword = () => {
    const lowerCaseChars = 'abcdefghijklmnopqrstuvwxyz';
    const uperCaseChars =  includeUppercase.value ?  'ABCDEFGHIJKLMNOPQRSTUVWXYZ' : '';
    const numbersChars = includeNumbers.value ? '0123456789' : '';
    const symbolChars = includeSymbols.value ? '!@#$%^&*()-_=+[]{}|;:,.<>?/' : '';

    const allChars = lowerCaseChars + uperCaseChars + numbersChars + symbolChars;

    let password = '';

    for (let i = 0; i < passwordLenght.value; i++) {
        const randomIndex = Math.floor(Math.random() * allChars.length)
        password += allChars[randomIndex];
    }
    generatedPassword.value = password;
}

</script>

 <template>
    <div>
        <h2>Password Generator</h2>
        <label for="lenght">Password Length</label>
        <input type="number" id="lenght" v-model="passwordLenght" min="4" max="32" />
        <br><br/>

        <label>Include UpperCase:</label>
        <input type="checkbox" id="includeUppercase" v-model="includeUppercase" />
        <br><br/>

        <label>Include Numbers:</label>
        <input type="checkbox" id="includeNumbers" v-model="includeNumbers" />

        <br><br/>

        <label>Include Symbols:</label>
        <input type="checkbox" id="includeSymbols" v-model="includeSymbols" />

        <button @click="generatePassword">Generator Password</button>

        <div v-if="generatedPassword">
            <strong>Your Password:</strong> {{ generatedPassword }}
        </div>
    </div>
 </template>