<script setup>

useHead({
  title: 'Password Generator',
  meta: [
    { name: 'description', content: 'A simple password generator using Vue and nuxt' },
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
})

import { ref, onMounted } from 'vue'

const smallLetter = 'abcdefghijklmnopqrstuvwxyz';
const capitalLetter = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
const numberCharacter = '0123456789';
const specialCharacters = '!@#$%^&*()_+[]{}|;:,.<>?';

const passwordLength = ref(4);
const includeSmallLetters = ref(true);
const includeCapitalLetters = ref(true);
const includeNumbers = ref(false);
const includeSpecialCharacters = ref(false);



// console.log(includeSmallLetters.value, includeCapitalLetters.value, includeNumbers.value, includeSpecialCharacters.value, passwordLength.value);

const generatePassword = () => {
  const base = Math.trunc(passwordLength.value / 4)
  const extra = passwordLength.value % 4;

  let password = '';






  console.log("button submit" + includeSmallLetters.value, includeCapitalLetters.value, includeNumbers.value, includeSpecialCharacters.value, passwordLength.value + "extra: " + extra + " base: " + base);

}

</script>

<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-sm-12 mt-5">
          <h2 class="text-center mb-4">Password Generator</h2>

          <div class="widthBox mx-auto  p-4">
            <div>
              <label class="fw-bold">Password Length</label>
              <input type="text" class="form-control fw-bold" style="width: 100px;" v-model="passwordLength">
              <hr>
            </div>
            <div class="mt-2">
              <div>
                <input type="checkbox" class="me-2" value="smallLetter" checked v-model="includeSmallLetters">
                <label for="">Include Small Letters</label>
              </div>
              <div>
                <input type="checkbox" class="me-2" value="capitalLetter" checked v-model="includeCapitalLetters">
                <label for="">Include Capital Letters</label>
              </div>
              <div>
                <input type="checkbox" class="me-2" value="numbers" v-model="includeNumbers">
                <label for="">Include Numbers</label>
              </div>
              <div>
                <input type="checkbox" class="me-2" id="specialCharacters" value="specialCharacters"
                  v-model="includeSpecialCharacters">
                <label for="">Include Special Characters</label>
              </div>
              <div class="text-center mt-3 ">
                <hr>
                <button class="fw-bold btn btn-success" @click="generatePassword"> Generate Passwrod </button>
              </div>
            </div>
          </div>

        </div>
      </div>
      <div class="row">
        <div class="row mt-5">
          <div class="col-sm-12 text-center">
            <button class="fw-bold btn btn-success" @click="generatePassword"> Generate Passwrod </button>
            <div class="border border-3 p-4 mt-5 text-dark  fw-bold ">sfs</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.widthBox {
  width: 300px;
  border: 1px solid #ccc;
}

input[type='checkbox'] {

  background: #d22;
  border: 1px solid #d22;
  box-shadow: inset 0 1px 2px 0 rgba(0, 0, 0, 0);
  height: 20px;
  width: 20px;
}
</style>
