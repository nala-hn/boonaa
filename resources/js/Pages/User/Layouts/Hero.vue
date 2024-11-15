<template>
    <section
        id="boonaa"
        class="relative w-full flex items-center justify-center overflow-hidden"
    >
        <img
            :src="heroBackgrounds[currentIndex]"
            alt="Hero Background"
            class="w-full h-[30vh] sm:h-[35vh] lg:h-[85vh] object-cover"
        />
        <div class="absolute inset-0 bg-black opacity-40"></div>
        <div
            class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex items-center space-x-2"
        >
            <button
                v-for="(bg, index) in heroBackgrounds"
                :key="index"
                @click="handleSelect(index)"
                :class="[
                    'w-1 h-1 md:w-2 md:h-2 rounded-full',
                    index === currentIndex ? 'bg-white' : 'bg-gray-500',
                ]"
            ></button>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const heroBackgrounds = [
    "/images/bg1.jpeg",
    "/images/bg2.jpeg",
    "/images/bg3.jpeg",
];

const currentIndex = ref(0);
let intervalId;

const setCarouselInterval = () => {
    intervalId = setInterval(() => {
        currentIndex.value = (currentIndex.value + 1) % heroBackgrounds.length;
    }, 5000);
};

const handleSelect = (index) => {
    currentIndex.value = index;
    clearInterval(intervalId);
    setCarouselInterval();
};

onMounted(setCarouselInterval);
onUnmounted(() => clearInterval(intervalId));
</script>
