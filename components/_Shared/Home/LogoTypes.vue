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
                <button @click="ddd" class="py-2 px-16 bg-slate-500 text-white mt-2 rounded xsx">pay</button>
            </div>
            <div v-if="isOpen" id="popup-modal" tabindex="-1"
                class="flex justify-center  bg-black/50 overflow-y-auto overflow-x-hidden fixed top-0 right-0 left-0 z-50 justify-center items-center w-full md:inset-0 h-[calc(100%-1rem)] max-h-full">
                <div class="relative p-4 w-full max-w-md max-h-full">
                    <div class="relative bg-white rounded-lg shadow-sm dark:bg-gray-700">
                        <button type="button"
                            class="absolute top-3 end-2.5 text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
                            data-modal-hide="popup-modal">
                            <svg @click="close" class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg"
                                fill="none" viewBox="0 0 14 14">
                                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                    stroke-width="2" d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6" />
                            </svg>
                            <span class="sr-only">Close modal</span>
                        </button>
                        <div class="p-4 md:p-5 text-center">
                            <svg class="mx-auto mb-4 text-gray-400 w-12 h-12 dark:text-gray-200" aria-hidden="true"
                                xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                    stroke-width="2" d="M10 11V6m0 8h.01M19 10a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
                            </svg>

                            <h3 class="mb-5 text-lg font-normal text-gray-500 dark:text-gray-400">Are you sure you want
                                to delete this product?</h3>
                            <button data-modal-hide="popup-modal" type="button"
                                class="text-white bg-red-600 hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 font-medium rounded-lg text-sm inline-flex items-center px-5 py-2.5 text-center">
                                Yes, I'm sure
                            </button>
                            <button data-modal-hide="popup-modal" type="button"
                                class="py-2.5 px-5 ms-3 text-sm font-medium text-gray-900 focus:outline-none bg-white rounded-lg border border-gray-200 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-4 focus:ring-gray-100 dark:focus:ring-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700">No,
                                cancel</button>
                        </div>
                    </div>
                </div>
            </div>

        </div>

    </section>


</template>
<script setup>
import { ref, onMounted } from 'vue';
const isOpen = ref(false)
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
const ddd = () => {
    isOpen.value = !isOpen.value

}
const close = () => {
    isOpen.value = false


}
</script>
<style scoped>
.bg-blacked {
    filter: grayscale(100%);


}

.xsx:hover {
    margin-top: 15px;
    transition: all 0.3s ease-in-out;
}
</style>