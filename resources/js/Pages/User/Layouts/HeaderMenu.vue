<script setup>
import { Link, usePage } from "@inertiajs/vue3";
import { ref, computed, onMounted, onUnmounted } from "vue";
import {
    Search,
    ShoppingCart,
    User,
    ArrowDown,
    Check,
    CircleCheck,
    CirclePlus,
    CirclePlusFilled,
    Plus,
} from "@element-plus/icons-vue";
import Color from "element-plus/es/components/color-picker/src/utils/color";

const canLogin = usePage().props.canLogin;
const canRegister = usePage().props.canRegister;
const auth = usePage().props.auth;
const cart = computed(() => usePage().props.cart);
const scrolled = ref(false);
const activePage = ref(false);
const isSearchActive = ref(false);
const searchQuery = ref("");
const searchContainer = ref(null);

const toggleSearch = () => {
    isSearchActive.value = !isSearchActive.value;
};

const handleOutsideClick = (event) => {
    if (
        searchContainer.value &&
        !searchContainer.value.contains(event.target)
    ) {
        isSearchActive.value = false;
    }
};

const setActive = (page) => {
    activePage.value = page;
};

const handleScroll = () => {
    scrolled.value = window.scrollY > 0;
};

onMounted(() => {
    window.addEventListener("scroll", handleScroll);
    document.addEventListener("click", handleOutsideClick);
});

onUnmounted(() => {
    window.removeEventListener("scroll", handleScroll);
    document.removeEventListener("click", handleOutsideClick);
});
</script>
<template>
    <nav
        :class="[
            'bg-black border-gray-200 dark:bg-gray-900 fixed w-full z-50 transition-colors duration-300',
            scrolled
                ? 'bg-white text-[#f594a7]'
                : 'bg-white text-[#f594a7]',
        ]"
    >
        <div
            class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4"
        >
            <Link :href="route('home')" class="flex items-center">
                <img
                    src="/images/boonaa_logo.png"
                    alt="boonaa id"
                    class="w-5 h-5 mr-[1px] mb-1"
                />

                <span
                    class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white"
                    >OONAA</span
                >
            </Link>
            <div v-if="canLogin" class="flex items-center md:order-2">
                <div class="relative mr-1" @click="handleOutsideClick">
                    <button
                        @click="toggleSearch"
                        class="relative inline-flex items-center p-2 text-sm font-medium text-center text-white bg-transparent opacity-55 rounded-full hover:bg-[#f89cae] focus:bg-[#f89cae] focus:ring-4 focus:outline-none focus:ring-red-100 dark:bg-blue-600 dark:hover:bg-pinkf dark:focus:ring-[#f89cae]"
                    >
                        <el-icon :color="scrolled ? 'black' : 'black'" :size="22"><Search /></el-icon>
                    </button>
                    <div
                        v-if="isSearchActive"
                        class="absolute top-0 right-10 -mt-2 bg-transparent p-2 rounded-lg"
                    >
                        <input
                            type="text"
                            v-model="searchQuery"
                            class="p-2 border rounded-md focus:bg-[#f89cae] focus:outline-none bg-transparent"
                            :class="{
                                'border-black': !scrolled,
                                'border-black': scrolled,
                                'focus:border-[#f494a7]': !scrolled,
                                'focus:ring-[#f494a7]': !scrolled,
                                'focus:border-black': scrolled,
                                'focus:ring-black': scrolled,
                            }"
                        />
                    </div>
                </div>

                <div class="mr-1" v-if="cart.data.count > 0">
                    <Link
                        :href="route('cart.view')"
                        class="relative inline-flex items-center p-2 text-sm font-medium text-center text-white bg-transparent opacity-55 rounded-full hover:bg-[#f89cae] focus:bg-[#f89cae] focus:ring-4 focus:outline-none focus:ring-red-100 dark:bg-blue-600 dark:hover:bg-pinkf dark:focus:ring-[#f89cae]"
                    >
                        <el-icon :color="scrolled ? 'black' : 'black'" :size="22"><ShoppingCart /></el-icon>

                        <span class="sr-only">cart</span>
                        <div
                            class="absolute inline-flex items-center justify-center w-6 h-6 text-xs font-bold text-white bg-red-500 border-2 border-transparent rounded-full -top-2 -right-2 dark:border-gray-900"
                        >
                            {{ cart.data.count }}
                        </div>
                    </Link>
                </div>
                <div class="ml-1">
                    <Link
                        :href="route('Guest')"
                        class="relative inline-flex items-center p-2 text-sm font-medium text-center text-white bg-transparent opacity-55 rounded-full hover:bg-[#f89cae] focus:bg-[#f89cae] focus:ring-4 focus:outline-none focus:ring-red-100 dark:bg-blue-600 dark:hover:bg-pinkf dark:focus:ring-[#f89cae]"
                    >
                        <el-icon :color="scrolled ? 'black' : 'black'" :size="22"><User /></el-icon>
                    </Link>
                </div>

                <!-- Dropdown menu -->
                <div
                    v-if="auth.user"
                    class="z-50 hidden my-4 text-base list-none bg-white divide-y divide-gray-100 rounded-lg shadow dark:bg-gray-700 dark:divide-gray-600"
                    id="user-dropdown"
                >
                    <div class="px-4 py-3">
                        <span
                            class="block text-sm text-gray-900 dark:text-white"
                            >{{ auth.user.name }}</span
                        >
                        <span
                            class="block text-sm text-gray-500 truncate dark:text-gray-400"
                            >{{ auth.user.email }}</span
                        >
                    </div>
                    <ul class="py-2" aria-labelledby="user-menu-button">
                        <li>
                            <Link
                                :href="route('dashboard')"
                                class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white"
                            >
                                Dashboard</Link
                            >
                        </li>

                        <li>
                            <Link
                                :href="route('logout')"
                                method="post"
                                class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white"
                            >
                                Sign out</Link
                            >
                        </li>
                    </ul>
                </div>
                <button
                    data-collapse-toggle="navbar-user"
                    type="button"
                    class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
                    aria-controls="navbar-user"
                    aria-expanded="false"
                >
                    <span class="sr-only">Open main menu</span>
                    <svg
                        class="w-5 h-5"
                        aria-hidden="true"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 17 14"
                    >
                        <path
                            stroke="currentColor"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M1 1h15M1 7h15M1 13h15"
                        />
                    </svg>
                </button>
            </div>
            <div
                class="items-center justify-between hidden w-full md:flex md:w-auto md:order-1"
                id="navbar-user"
            >
                <ul
                    class="flex flex-col font-medium p-4 md:p-0 mt-4 border border-gray-100 rounded-lg md:flex-row md:space-x-8 md:mt-0 md:border-0 md:dark:bg-gray-900 dark:border-gray-700"
                >
                    <li>
                        <a
                            href="#"
                            :class="[
                                'block py-2 pl-3 pr-4 rounded md:bg-transparent md:p-0 md:dark:text-pinkf',
                                scrolled ? 'text-black' : 'text-black',
                                scrolled ? 'bg-transparent' : 'bg-pinkf',

                                activePage === 'all'
                                    ? 'text-pinkf border-b-2 border-[#f494a7]'
                                    : '',
                            ]"
                            @click="setActive('all')"
                            aria-current="page"
                        >
                            All
                        </a>
                    </li>
                    <li>
                        <a
                            href="#"
                            :class="[
                                'block py-2 pl-3 pr-4 rounded md:bg-transparent md:p-0 md:dark:text-pinkf',
                                scrolled ? 'text-black' : 'text-black',
                                scrolled ? 'bg-transparent' : 'bg-pinkf',

                                activePage === 'newArrivals'
                                    ? 'text-pinkf border-b-2 border-[#f494a7]'
                                    : '',
                            ]"
                            @click="setActive('newArrivals')"
                            >New Arrivals</a
                        >
                    </li>
                    <li>
                        <el-dropdown>
                            <span
                                :class="[
                                    'el-dropdown-link py-2 pl-3 pr-4 rounded-none md:p-0 no-border',
                                    scrolled ? 'text-black' : 'text-black',
                                    scrolled
                                        ? 'md:text-black'
                                        : 'md:text-black',
                                    scrolled
                                        ? 'dark:text-gray-300'
                                        : 'dark:text-black',
                                    isActive
                                        ? 'text-[#f494a7]'
                                        : 'text-[#f494a7]',
                                    'hover:bg-pinkf active:bg-pinkf',
                                ]"
                                @click="setActive"
                            >
                                Categories
                                <el-icon class="el-icon--right">
                                    <arrow-down />
                                </el-icon>
                            </span>
                            <template #dropdown>
                                <el-dropdown-menu>
                                    <el-dropdown-item :icon="Plus"
                                        >Action 1</el-dropdown-item
                                    >
                                    <el-dropdown-item :icon="CirclePlusFilled">
                                        Action 2
                                    </el-dropdown-item>
                                    <el-dropdown-item :icon="CirclePlus"
                                        >Action 3</el-dropdown-item
                                    >
                                    <el-dropdown-item :icon="Check"
                                        >Action 4</el-dropdown-item
                                    >
                                    <el-dropdown-item :icon="CircleCheck"
                                        >Action 5</el-dropdown-item
                                    >
                                </el-dropdown-menu>
                            </template>
                        </el-dropdown>
                    </li>
                    <li>
                        <a
                            href="#"
                            :class="[
                                'block py-2 pl-3 pr-4 rounded md:bg-transparent md:p-0 md:dark:text-pinkf',
                                scrolled ? 'text-black' : 'text-black',
                                scrolled ? 'bg-transparent' : 'bg-pinkf',

                                activePage === 'bestSeller'
                                    ? 'text-pinkf border-b-2 border-[#f494a7]'
                                    : '',
                            ]"
                            @click="setActive('bestSeller')"
                            >Best Seller</a
                        >
                    </li>
                    <li>
                        <a
                            href="#"
                            :class="[
                                'block py-2 pl-3 pr-4 rounded md:bg-transparent md:p-0 md:dark:text-pinkf',
                                scrolled ? 'text-black' : 'text-black',
                                scrolled ? 'bg-transparent' : 'bg-pinkf',

                                activePage === 'exclusiveSales'
                                    ? 'text-pinkf border-b-2 border-[#f494a7]'
                                    : '',
                            ]"
                            @click="setActive('exclusiveSales')"
                            >Exclusive Sales</a
                        >
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</template>
