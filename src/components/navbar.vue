<script setup>
   import { ref } from 'vue';
   import { database } from '../server'
   import Modal from "./modal.vue"

   const emits = defineEmits(['openModal'])

   const isAuthenticated = ref(false)
   const curentFullname = ref("")

   const isModalShow = ref(false)

   const openModal = () => {
    emits('openModal')
    isModalShow.value = true
   }
   defineProps({
    color:"",
    isValid: false
   })

   const openModalLogin = () => {
    emits("openModal")
    isModalShow.value = true
    isLogin.value = true
   }

   const openModalRegister = () => {
    emits("openModal")
    isModalShow.value = true
    isLogin.value = false
   }

   const isLogin = ref(false)

   const fullname = ref("")
   const email = ref("")
   const password = ref("")
   const username = ref("")
   const cpassword = ref("")

   const isFormValid = () => {
    return email.value.includes("@") && email.value.length > 5 && password.value.length > 6
   }

   const isFormRegistValid = () => {
    return fullname.value.length > 2 && email.value.includes("@") && email.value.length > 5 && password.value.length > 6 && password.value === cpassword.value
   }


   const submitLogin = () => {
    curentFullname.value = database.value.filter((x) => x.email === email.value).map((x) => x.fullname)[0]
    isModalShow.value = false
    isAuthenticated.value = true
    email.value = ""
    password.value = ""
   }

   const submitRegister = () => {
       const payLoad = {
        id: new Date(),
        username: username.value,
        email: email.value,
        fullname: fullname.value,
    }
    database.value.push(payLoad)
    isModalShow.value = false,
    email.value = "",
    password.value = ""
   }

    const isLogout = () => {
        curentFullname.value,
        isAuthenticated.value = false
    }
</script>
<template>
<header class="sticky top-0">
    <nav class="bg-white w-screen h-[15vh] drop-shadow-xl flex">
            <div class="w-[10vw] flex justify-end items-center">
                <img src="./img/drivi(1).png" alt="" class="h-[45px]">
            </div>
            <div class="w-[9vw] pl-[1vw] flex items-center">
                <a href="#" class="font-custom text-5xl">Drivi</a>
            </div>
            <div class="w-[78vw]">
                <ul class="pr-[2vw] h-[15vh] flex gap-[2vw] justify-end items-center">
                    <router-link to="/">
                    <li><a href="#" class="font-custom text-xl p-[1vw] rounded-[1vw] hover:bg-blue-700 hover:text-white hover:duration-500">Home</a></li>
                    </router-link>
                    <router-link to="/service">
                    <li><a href="#" class="font-custom text-xl p-[1vw] rounded-[1vw] hover:bg-blue-700 hover:text-white hover:duration-500">Services</a></li>
                    </router-link>

                    <div class="flex" v-if="isAuthenticated">
                    <li>
                        <a class="font-custom text-xl p-[1vw] rounded-[1vw] hover:bg-blue-700 hover:text-white hover:duration-500">{{ curentFullname }}</a></li>
                    <li><span @click="isLogout()"><a class="font-custom text-xl p-[1vw] rounded-[1vw] hover:bg-blue-700 hover:text-white hover:duration-500">Logout</a></span></li>
                    </div>

                    <div class="flex" v-else>
                    <li><a @click="openModalRegister()" class="font-custom text-xl p-[1vw] rounded-[1vw] hover:bg-blue-700 hover:text-white hover:duration-500">Register</a></li>
                    <li><span @click="openModalLogin()"><a class="font-custom text-xl p-[1vw] rounded-[1vw] hover:bg-blue-700 hover:text-white hover:duration-500">Login</a></span></li>
                    </div>
                </ul> 
            </div>
        </nav>
</header>
<Modal v-if="isModalShow" @close-modal="isModalShow = false" :title="isLogin ? 'Login' : 'Register'" :btnText="isLogin ? 'Login' : 'Register'" :isValid="isLogin ? !isFormValid() : !isFormRegistValid()" @submit-modal="isLogin ? submitLogin() : submitRegister()">
<div class="w-full p-4">
   
<form>
  <div class="mb-6" v-if="!isLogin">
    <label for="text" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Your Fullname</label>
    <input v-model="fullname" type="username" id="text" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="your name" required="">
  </div>
    <div class="mb-6">
    <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Your Email</label>
    <input v-model="email" type="email" id="password" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="your Email" required="">
  </div>
  <div class="mb-6">
    <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Your password</label>
    <input v-model="password" type="password" id="password" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="your password" required="">
  </div>
   <div class="mb-6" v-if="!isLogin">
    <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Confirm passowrd</label>
    <input v-model="cpassword" type="password" id="text" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="your Fullname" required="">
  </div>

  <div class="flex items-start mb-6">
  </div>
</form>

  <p class="text-center text-gray-500 text-xs">
    &copy;2020 Acme Corp. All rights reserved.
  </p>
</div>
</Modal>
</template>