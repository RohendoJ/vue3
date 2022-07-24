<script setup>
import {ref} from "vue"
import Navbar from '../components/navbar.vue'
import Banner from '../components/banner.vue'

const isDescShow = ref(false)
const isModalShow = ref(false)

</script>
<template>
    <Navbar @open-modal="isModalShow = true"/>
    <Banner title="Home" color="bg-sky-50" desc="asdhaoisdhaoidhaoi" 
    @click="isDescShow = !isDescShow" :is-show="isDescShow"/>
</template>