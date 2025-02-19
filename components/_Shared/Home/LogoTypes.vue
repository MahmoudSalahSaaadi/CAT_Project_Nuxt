<template>
    <main class=" py-[70px] px-[135px] w-full">
        <div class="flex justify-between gap-[95px] w-full">
            <div :key="index" v-for="(image, index) in images" class="flex">
                <img :src="`/images/design/home/${image}`" :alt="`Image ${index + 1}`" />
            </div>
        </div>
    </main>
</template>
<script setup>
const images = [
    'Company logo (1).svg',
    'Company logo (3).svg',
    'Company logo (4).svg',
    'Vector (3).svg',
    'Company logo (5).svg',
    'Company logo.svg'
];
</script>