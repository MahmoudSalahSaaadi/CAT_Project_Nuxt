<script setup>
import { ref } from "vue";
const localePath = useLocalePath()
const menuLinks = ref([
    {
        name: "About us",
        path: "about"
    },
    {
        name: "Services",
        path: "/"
    },
    {
        name: "Use Cases",
        path: "/"
    },
    {
        name: "Pricing",
        path: "/"
    },
    {
        name: "Blog",
        path: "/"
    },

])
</script>

<template>
    <header class="w-full  max-auto py-20 px-[135px]">
        <nav class="flex justify-between items-center w-full h-[68px] ">
            <figure>
                <img src="/images/design/home/Logo.svg" alt="Logo">
            </figure>
            <div class="flex items-center gap-10">
                <ul class="flex items-center gap-10">
                    <li class="text-black text-xl font-display" v-for="link in menuLinks" :key="link.name">
                        <NuxtLink :to="localePath(link.path)">{{ link.name }}</NuxtLink>
                    </li>
                </ul>
                <button
                    class="border border-black text-black py-[20px] px-[35px] rounded-lg font-display text-xl">Request a
                    quote</button>
            </div>
        </nav>
    </header>
</template>
