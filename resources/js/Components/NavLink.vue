<script setup>
import { computed } from 'vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
    href: {
        type: String,
        required: true,
    },
    active: {
        type: Boolean,
    },
});

const classes = computed(() =>
    props.active
        ? 'inline-flex items-center px-1 border-b-2 border-[#f494a7] text-[16px] font-medium leading-5 text-pinkf focus:outline-none focus:border-[#f494a7] transition duration-150 ease-in-out'
        : 'inline-flex items-center px-1 border-b-2 border-transparent text-[16px] font-medium leading-5 text-gray-500 hover:text-gray-700 hover:border-gray-300 focus:outline-none focus:text-gray-700 focus:border-gray-300 transition duration-150 ease-in-out'
);
</script>

<template>
    <Link :href="href" :class="classes">
        <slot />
    </Link>
</template>
