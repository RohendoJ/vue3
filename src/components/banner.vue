<script setup>
    defineProps({
        title: "",
        color: "",
        desc: "",
        image: "",
        isShow: false,
    })
</script>

<template>
    <main :class="color" class="w-full h-[85vh] flex">
            <div class="w-[50vw] h-[85vh] flex">
                <img src="./img/main.png" alt="">
                <img :src="image" width="500">
            </div>
            <div class="w-[50vw] h-[85vh] flex-col" v-if="isShow">
                <div class="w-[50vw] h-[37.3vh] flex justify-center items-end">
                    <h1 class="font-custom text-5xl">Drivi</h1>
                </div>
                <div class="w-[50vw] h-[10vh] flex-col flex justify-center items-center">
                    <p>{{ desc }}</p>
                    <input class="file:bg-blue-500 file:border-0 file:text-white file:rounded-full file:cursor-pointer file:duration-500 file:hover:bg-blue-700" type="file" name="" id="">
                </div>
                <div class="w-[50vw] h-[37.3vh] flex-col flex justify-start items-center">
                    <button class="bg-blue-500 w-[5vw] h-[5vh] rounded-md text-white duration-500 hover:bg-blue-700">Upload</button>
                </div>
            <h1>{{ title }}</h1>
            </div>
        </main>     
</template>