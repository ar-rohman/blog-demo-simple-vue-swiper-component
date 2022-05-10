<script setup>
import { ref } from 'vue'

const carousel = ref();
const showLeftButton = ref(false);
const showRightButton = ref(true);

const scrollTo = (direction) => {
    const { width } = carousel.value.getBoundingClientRect();
    const scrollWidth = carousel.value.scrollWidth;
    let scrollLeft = carousel.value.scrollLeft;
    scrollLeft = direction === 'left' ? scrollLeft - width : scrollLeft + width;
    carousel.value.scroll({
        left: scrollLeft,
        behavior: 'smooth',
    });
    showLeftButton.value = scrollLeft > 0;
    showRightButton.value = scrollLeft < scrollWidth - width;
}
</script>

<template>
    <div class="relative">
        <button
            v-if="showLeftButton"
            class="border shadow-md bg-white p-2 rounded-full z-20 absolute top-1/2 -left-5 -translate-y-1/2 transform transition motion-safe:hover:scale-110 duration-500"
            @click="scrollTo('left')">
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                <path d="M13.36 17a1 1 0 0 1-.72-.31l-3.86-4a1 1 0 0 1 0-1.4l4-4a1 1 0 1 1 1.42 1.42L10.9 12l3.18 3.3a1 1 0 0 1 0 1.41 1 1 0 0 1-.72.29z" />
            </svg>
        </button>
        <div ref="carousel" class="flex overflow-x-auto hide-scrollbar">
            <div class="flex gap-4 m-[3px]">
                <slot></slot>
            </div>
        </div>
        <button
            v-if="showRightButton"
            class="border shadow-md bg-white p-2 rounded-full z-20 absolute top-1/2 -right-5 -translate-y-1/2 transform transition motion-safe:hover:scale-110 duration-500"
            @click="scrollTo('right')">
            <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                <path d="M10.5 17a1 1 0 0 1-.71-.29 1 1 0 0 1 0-1.42L13.1 12 9.92 8.69a1 1 0 0 1 0-1.41 1 1 0 0 1 1.42 0l3.86 4a1 1 0 0 1 0 1.4l-4 4a1 1 0 0 1-.7.32z" />
            </svg>
        </button>
    </div>
</template>
