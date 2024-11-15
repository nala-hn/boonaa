<script setup>
import { onMounted } from 'vue'
import { initFlowbite } from 'flowbite'
import HeaderMenu from './HeaderMenu.vue';
import Hero from './Hero.vue';

// initialize components based on data attribute selectors
onMounted(() => {
    initFlowbite();
})



</script>
<template>
    <!-- header -->
    <HeaderMenu></HeaderMenu>
    <!-- end -->
    <!-- main content -->
    
    <slot />
    <!-- end -->
    
</template>
