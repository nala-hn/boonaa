<script setup>
import HeaderMenu from "@/Pages/User/Layouts/HeaderMenu.vue";
import { Link, usePage } from '@inertiajs/vue3';
import Login from "../Auth/Login.vue";
import { computed } from 'vue'
const canLogin = usePage().props.canLogin;
const canRegister = usePage().props.canRegister;
const auth = usePage().props.auth;
const cart = computed(() => usePage().props.cart);


</script>

<template>
    <HeaderMenu></HeaderMenu>
    <div
        class="min-h-screen flex flex-col sm:justify-center items-center pt-6 sm:pt-0 bg-gray-100"
    >
        <div class="flex flex-col items-center mb-6">
            <span>Dapatkan layanan VIP dengan login 1-klik:</span>
            <span>Kamu bisa chat dengan OcloOfficial.</span>
            <span>★ Jadilah yang pertama mendapat diskon khusus.</span>
            <span>★ Jangan pernah kehilangan order kamu.</span>
        </div>

        <div v-if="canLogin" class="flex items-center md:order-2">
            
        </div>

        <button
            v-if="auth.user"
            type="button"
            class="flex mr-3 text-sm bg-gray-800 rounded-full md:mr-0 focus:ring-4 focus:ring-gray-300 dark:focus:ring-gray-600"
            id="user-menu-button"
            aria-expanded="false"
            data-dropdown-toggle="user-dropdown"
            data-dropdown-placement="bottom"
        >
            <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                class="w-8 h-8 rounded-full bg-white"
                stroke="currentColor"
            >
                <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M15.75 6a3.75 3.75 0 11-7.5 0 3.75 3.75 0 017.5 0zM4.501 20.118a7.5 7.5 0 0114.998 0A17.933 17.933 0 0112 21.75c-2.676 0-5.216-.584-7.499-1.632z"
                />
            </svg>
        </button>
        <div v-else>
            <Link
                :href="route('login')"
                type="button"
                
            >
            <Login></Login>    
            </Link
            >
            <Link
                :href="route('register')"
                v-if="canRegister"
                type="button"
                class="text-white bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
            >
                Register</Link
            >
        </div>

        <div
            class="w-full sm:max-w-md mt-6 bg-white shadow-md overflow-hidden sm:rounded-lg"
        >
            <slot />
        </div>
    </div>
</template>
