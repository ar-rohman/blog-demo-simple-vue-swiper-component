<script setup>
import { ref, onMounted } from 'vue';
import SimpleCarousel from './components/SimpleCarousel.vue';
import products from './data/products.json';

const data = ref();
const fetchData = async () => {
    // const result = await fetch('https://fakestoreapi.com/products');
    // data.value = await result.json();
    data.value = products;

}
onMounted(fetchData);
</script>

<template>
    <div class="max-w-screen-lg mx-auto">
        <header class="border-b py-4 mx-10">
            <img alt="Vue logo" src="./assets/logo.png" class="w-12" />
        </header>
        <main class="mt-4 mx-10">
            <p class="mb-2 font-semibold">Product Carousel</p>
            <simple-carousel>
                <div
                    v-for="item in data"
                    :key="item.id"
                    class="rounded-2xl relative w-44 shadow">
                    <img
                        :src="item.image"
                        class="w-full h-44 rounded-t-2xl object-cover object-top"
                        :alt="item.title" />
                    <div class="pt-2 pb-4 px-3 text-sm flex flex-col gap-y-2">
                        <p class="line-clamp-2">{{ item.title }}</p>
                        <p class="font-medium">${{ item.price }}</p>
                        <div class="bg-emerald-100 px-2 py-1 text-xs w-max rounded-lg text-emerald-600 font-semibold">{{ item.category }}</div>
                        <div class="flex items-center">
                            <svg class="w-4 h-4 text-yellow-500" viewBox="0 0 24 24">
                                <path d="M17.56 21a1 1 0 0 1-.46-.11L12 18.22l-5.1 2.67a1 1 0 0 1-1.45-1.06l1-5.63-4.12-4a1 1 0 0 1-.25-1 1 1 0 0 1 .81-.68l5.7-.83 2.51-5.13a1 1 0 0 1 1.8 0l2.54 5.12 5.7.83a1 1 0 0 1 .81.68 1 1 0 0 1-.25 1l-4.12 4 1 5.63a1 1 0 0 1-.4 1 1 1 0 0 1-.62.18z" fill="currentColor" />
                            </svg>
                            <p class="ml-2 text-xs">{{ item.rating.rate }} | {{ item.rating.count }} Reviews</p>
                        </div>
                    </div>
                </div>
            </simple-carousel>
        </main>
    </div>
</template>
