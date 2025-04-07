<template>
    <section class=" py-[70px] px-[135px] w-full">
        <div class="flex justify-between gap-[95px] w-full">
            <div :key="index" v-for="(image, index) in images" class="flex">
                <img class="bg-blacked" :src="`/images/design/home/${image}`" :alt="`Image ${index + 1}`" />
            </div>
        </div>
        <div class="grid grid-cols-4 gap-4 w-full mt-4 ">
            <div class="border border-red-200 p-4 rounded-lg hover:bg-red-200 hover:obacity-50" v-for="aa in data"
                :key="aa.id">
                <img class="w-[150px]" :src="aa.image" alt="">
                <p>{{ aa.price }}</p>
                <p>{{ aa.title }}</p>
                <button class="py-2 px-16 bg-slate-500 text-white mt-2 rounded ">pay</button>
            </div>

        </div>
    </section>

</template>
<script setup>
import { ref, onMounted } from 'vue';

const images = [
    'Company logo (1).svg',
    'Company logo (3).svg',
    'Company logo (4).svg',
    'Vector (3).svg',
    'Company logo (5).svg',
    'Company logo.svg'
]

const data = ref(null);
// const error = ref(null);

const fetchData = async () => {
    const response = await fetch('https://fakestoreapi.com/products');
    data.value = await response.json();
};

onMounted(() => {
    fetchData();
});
</script>
<style scoped>
.bg-blacked {
    filter: grayscale(100%);
}
</style>