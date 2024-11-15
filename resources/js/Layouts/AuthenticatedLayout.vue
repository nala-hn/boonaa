<script setup>
import { ref } from "vue";
import Dropdown from "@/Components/Dropdown.vue";
import DropdownLink from "@/Components/DropdownLink.vue";
import NavLink from "@/Components/NavLink.vue";
import ResponsiveNavLink from "@/Components/ResponsiveNavLink.vue";
import { Link } from "@inertiajs/vue3";
import { User, ArrowDown } from "@element-plus/icons-vue";

const showingNavigationDropdown = ref(false);
</script>

<template>
    <div>
        <div class="min-h-screen bg-gray-100">
            <nav class="bg-white border-b border-gray-100">
                <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                    <div class="flex justify-between h-16">
                        <div class="flex w-full">
                            <div class="shrink-0 flex items-center">
                                <Link
                                    :href="route('dashboard')"
                                    class="flex items-center"
                                >
                                    <img
                                        src="/images/boonaa_logo.png"
                                        alt="boonaa id"
                                        class="w-5 h-5 mr-[1px] mb-1"
                                    />
                                    <span
                                        class="self-center text-2xl font-semibold whitespace-nowrap text-pinkf"
                                        >OONAA</span
                                    >
                                </Link>
                            </div>

                             <div class="flex flex-col justify-center items-center w-full">
                            <div
                                class="hidden items-center space-x-8 space-y-auto sm:-my-px sm:flex"
                            >
                                <NavLink
                                    :href="route('dashboard')"
                                    :active="route().current('dashboard')"
                                    class="flex font-medium items-center"
                                >
                                    All
                                </NavLink>
                                <NavLink
                                    :href="route('profile.edit')"
                                    :active="route().current('profile.edit')"
                                    class="flex items-center"
                                >
                                    New Arrivals
                                </NavLink>
                                <NavLink>
                                    <el-dropdown>
                                        <span
                                            :class="[
                                                'el-dropdown-link pr-4 rounded-none md:p-0 no-border text-gray-500',
                                            ]"
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
                                                <el-dropdown-item
                                                    :icon="CirclePlusFilled"
                                                >
                                                    Action 2
                                                </el-dropdown-item>
                                                <el-dropdown-item
                                                    :icon="CirclePlus"
                                                    >Action 3</el-dropdown-item
                                                >
                                                <el-dropdown-item :icon="Check"
                                                    >Action 4</el-dropdown-item
                                                >
                                                <el-dropdown-item
                                                    :icon="CircleCheck"
                                                    >Action 5</el-dropdown-item
                                                >
                                            </el-dropdown-menu>
                                        </template>
                                    </el-dropdown>
                                </NavLink>
                                <NavLink
                                    :href="route('profile.edit')"
                                    :active="route().current('profile.edit')"
                                    class="flex items-center"
                                >
                                    Best Seller
                                </NavLink>
                                <NavLink
                                    :href="route('profile.edit')"
                                    :active="route().current('profile.edit')"
                                    class="flex items-center"
                                >
                                    Exclusive Sales
                                </NavLink>
                            </div>
                        </div>
                        </div>

                        <div class="hidden sm:flex sm:items-center sm:ml-6">
                            <div class="ml-3 relative">
                                <Dropdown :align="right" width="48">
                                    <template #trigger>
                                        <span class="inline-flex rounded-md">
                                            <button
                                                type="button"
                                                class="inline-flex items-center p-2 border border-transparent rounded-full text-gray-500 bg-white focus:outline-none transition ease-in-out duration-150 bg-transparent opacity-55 rounded-full hover:bg-[#f89cae] focus:bg-[#f89cae]"
                                            >
                                                <el-icon
                                                    color="black"
                                                    :size="22"
                                                    ><User
                                                /></el-icon>
                                            </button>
                                        </span>
                                    </template>

                                    <template #content>
                                        <DropdownLink
                                            :href="route('profile.edit')"
                                        >
                                            Profile
                                            {{
                                                $page.props.auth.user.name
                                            }}</DropdownLink
                                        >
                                        <DropdownLink
                                            :href="route('logout')"
                                            method="post"
                                            as="button"
                                        >
                                            Log Out
                                        </DropdownLink>
                                    </template>
                                </Dropdown>
                            </div>
                        </div>

                        <!-- Hamburger -->
                        <div class="-mr-2 flex items-center sm:hidden">
                            <button
                                @click="
                                    showingNavigationDropdown =
                                        !showingNavigationDropdown
                                "
                                class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:bg-gray-100 focus:text-gray-500 transition duration-150 ease-in-out"
                            >
                                <svg
                                    class="h-6 w-6"
                                    stroke="currentColor"
                                    fill="none"
                                    viewBox="0 0 24 24"
                                >
                                    <path
                                        :class="{
                                            hidden: showingNavigationDropdown,
                                            'inline-flex':
                                                !showingNavigationDropdown,
                                        }"
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M4 6h16M4 12h16M4 18h16"
                                    />
                                    <path
                                        :class="{
                                            hidden: !showingNavigationDropdown,
                                            'inline-flex':
                                                showingNavigationDropdown,
                                        }"
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M6 18L18 6M6 6l12 12"
                                    />
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Responsive Navigation Menu -->
                <div
                    :class="{
                        block: showingNavigationDropdown,
                        hidden: !showingNavigationDropdown,
                    }"
                    class="sm:hidden"
                >
                    <div class="pt-2 pb-3 space-y-1">
                        <ResponsiveNavLink
                            :href="route('dashboard')"
                            :active="route().current('dashboard')"
                        >
                            Boonaa.id
                        </ResponsiveNavLink>
                    </div>

                    <!-- Responsive Settings Options -->
                    <div class="pt-4 pb-1 border-t border-gray-200">
                        <div class="px-4">
                            <div class="font-medium text-base text-gray-800">
                                {{ $page.props.auth.user.name }}
                            </div>
                            <div class="font-medium text-sm text-gray-500">
                                {{ $page.props.auth.user.email }}
                            </div>
                        </div>

                        <div class="mt-3 space-y-1">
                            <ResponsiveNavLink :href="route('profile.edit')">
                                Profile
                            </ResponsiveNavLink>
                            <ResponsiveNavLink
                                :href="route('logout')"
                                method="post"
                                as="button"
                            >
                                Log Out
                            </ResponsiveNavLink>
                        </div>
                    </div>
                </div>
            </nav>

            <!-- Page Heading -->
            <header class="bg-white shadow" v-if="$slots.header">
                <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
                    <slot name="header" />
                </div>
            </header>

            <!-- Page Content -->
            <main>
                <slot />
            </main>
        </div>
    </div>
</template>
