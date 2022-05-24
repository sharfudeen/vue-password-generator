<script>
import { computed } from 'vue'

export default {
    data() {
        return {
            generatedPassword: '',
            uppercase: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
            lowercase: "abcdefghijklmnopqrstuvwxyz",
            numbers: "0123456789",
            specialCharacters: "!@#$%^&*()_+~`|}{[]:;?><,./-=",
            passLength: 12,
            isUppercase: true,
            isLowercase: true,
            isNumbers: true,
            isSymbols: true,
        }
    },
    methods: {
        generatePassword() {
            this.generatedPassword = '';
            let len = this.getString.length;
            for (let i = 0; i < this.passLength; i++) {
                this.generatedPassword += this.getString.charAt(Math.random() * len);
            }
        },
        copy() {
            navigator.clipboard.writeText(this.generatedPassword);
        }
    },
    computed: {
        getString() {
            let str = "";
            if (this.isUppercase) {
                str += this.uppercase;
            }
            if (this.isLowercase) {
                str += this.lowercase;
            }
            if (this.isSymbols) {
                str += this.specialCharacters;
            }
            if (this.isNumbers) {
                str += this.numbers;
            }
            return str;
        }
    }
}
</script>

<template>
    <div>
        <h1>Password Generator</h1>
        <div>
            <input name="generatedPassword" id="generatedPassword" :value="generatedPassword"
                placeholder="Your random password will appear here" />
            <button type="button" @click="copy">Copy</button>
        </div>
        <div>
            <label for="uppercase"> Uppercase </label>
            <input type="checkbox" name="uppercase" id="uppercase" v-model="isUppercase" />
        </div>
        <div>
            <label for="lowercase"> Lowercase </label>
            <input type="checkbox" name="lowercase" id="lowercase" v-model="isLowercase" />
        </div>
        <div>
            <label for="numbers"> Numbers </label>
            <input type="checkbox" name="numbers" id="numbers" v-model="isNumbers" />
        </div>
        <div>
            <label for="symbols"> Symbols </label>
            <input type="checkbox" name="symbols" id="symbols" v-model="isSymbols" />
        </div>
        <div>
            <label for="length"> Length </label>
            <input type="number" name="length" id="length" :value="passLength" />
        </div>
        <div>
            <button @click="generatePassword()">Gernerate</button>
        </div>
    </div>
</template>