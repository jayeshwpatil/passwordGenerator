<script setup>
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
const finalPassword = ref('');

onMounted(() => {
  generatePassword();
})

const generatePassword = () => {
  //set number find out which characters are selected and divide the password length by the number of selected character types
  // then find the base length of each character type and the extra characters that need to be added
  const setNumber =
    Number(includeSmallLetters.value) +
    Number(includeCapitalLetters.value) +
    Number(includeNumbers.value) +
    Number(includeSpecialCharacters.value);
  console.log("setNumber " + setNumber);

  const base = Math.trunc(passwordLength.value / setNumber)
  const extra = passwordLength.value % setNumber;

  const password = [];
  const randomNumber = (k) => k[Math.floor(Math.random() * k.length)];   //for generating random character from the string

  if (includeSmallLetters.value == true) {
    for (let i = 0; i < base; i++) {
      password.push(randomNumber(smallLetter))
    }
  }
  if (includeCapitalLetters.value == true) {
    for (let i = 0; i < base; i++) {
      password.push(randomNumber(capitalLetter))
    }
  }
  if (includeNumbers.value == true) {
    for (let i = 0; i < base; i++) {
      password.push(randomNumber(numberCharacter))
    }
  }
  if (includeSpecialCharacters.value == true) {
    for (let i = 0; i < base; i++) {
      password.push(randomNumber(specialCharacters))
    }
  }

  let randomCharacter = [];
  if (extra > 0) {
    const extraCharacters = [smallLetter, capitalLetter, numberCharacter, specialCharacters].filter((x, index) => {
      return (index == 0 && includeSmallLetters.value) ||
        (index == 1 && includeCapitalLetters.value) ||
        (index == 2 && includeNumbers.value) ||
        (index == 3 && includeSpecialCharacters.value);
    })

    for (let i = 0; i < extra; i++) {
      randomCharacter = randomNumber(extraCharacters)
      password.push(randomNumber(randomCharacter))
    }

  }
  console.log("password " + password);
  password.sort(() => Math.random() - 0.5)
  finalPassword.value = password.join('');

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

      <span
        class="widthBox mx-auto p-4  d-flex justify-content-center align-items-center text-dark fw-bold bg-danger text-white"
        style=" height:100px; max-width:100% !important; font-size:24px;">
        <span>{{ finalPassword }}</span>
      </span>


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
