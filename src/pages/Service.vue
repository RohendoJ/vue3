<script setup>
import Navbar from '../components/navbar.vue'
import Banner from '../components/banner.vue'
import Linux from '../components/img/linux.png'
</script>
<template>
    <Navbar />
    <Banner title="Home" :image="Linux" color="bg-yellow-400"/>
</template>