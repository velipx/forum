<script setup>
import { ref } from 'vue'
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue'
import {
    Dialog,
    DialogOverlay,
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    TransitionChild,
    TransitionRoot,
} from '@headlessui/vue'
import {
    BellIcon,
    CalendarIcon,
    ChartBarIcon,
    FolderIcon,
    HomeIcon,
    InboxIcon,
    Bars3Icon,
    UsersIcon,
    XMarkIcon,
    ChevronDownIcon,
} from '@heroicons/vue/24/outline'
import { MagnifyingGlassCircleIcon } from '@heroicons/vue/20/solid'

const navigation = [
    { name: 'Dashboard', href: '#', icon: HomeIcon, current: true },
    { name: 'Team', href: '#', icon: UsersIcon, current: false },
    {
        name: 'Projects',
        href: '#',
        icon: FolderIcon,
        current: false,
        children: [
            { name: 'Overview', href: '#' },
            { name: 'Calendar', href: '#' },
            { name: 'Settings', href: '#' },
        ],
    },
    {
        name: 'Calendar',
        href: '#',
        icon: CalendarIcon,
        current: false ,
        children: [
            { name: 'Overview', href: '#' },
            { name: 'Members', href: '#' },
        ],
    },
    { name: 'Documents', href: '#', icon: InboxIcon, current: false },
    { name: 'Reports', href: '#', icon: ChartBarIcon, current: false },
]

const userNavigation = [
    { name: 'Your Profile', href: '#' },
    { name: 'Settings', href: '#' },
    { name: 'Sign out', href: '#' },
]

const sidebarOpen = ref(false)
</script>

<template>
    <div class="text-white">
        <TransitionRoot as="template" :show="sidebarOpen">
            <Dialog as="div" class="fixed inset-0 flex z-40 md:hidden" @close="sidebarOpen = false">
                <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100" leave-to="opacity-0">
                    <DialogOverlay class="fixed inset-0 bg-gray-600 bg-opacity-75" />
                </TransitionChild>
                <TransitionChild as="template" enter="transition ease-in-out duration-300 transform" enter-from="-translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0" leave-to="-translate-x-full">
                    <div class="relative flex-1 flex flex-col max-w-xs w-full pt-5 pb-4 bg-gray-800">
                        <TransitionChild as="template" enter="ease-in-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in-out duration-300" leave-from="opacity-100" leave-to="opacity-0">
                            <div class="absolute top-0 right-0 -mr-12 pt-2">
                                <button type="button" class="ml-1 flex items-center justify-center h-10 w-10 rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white" @click="sidebarOpen = false">
                                    <span class="sr-only">Close sidebar</span>
                                    <XMarkIcon class="h-6 w-6 text-white" aria-hidden="true" />
                                </button>
                            </div>
                        </TransitionChild>
                        <div class="items-center px-4">
                            <Link :href="route('home')">
                                <ApplicationLogo />
                            </Link>
                        </div>
                        <div class="mt-5 flex-1 h-0 overflow-y-auto">
                            <nav class="px-2 space-y-1">
                                <a v-for="item in navigation" :key="item.name" :href="item.href" :class="[item.current ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white', 'group flex items-center px-2 py-2 text-base font-medium rounded-md']">
                                    <component :is="item.icon" :class="[item.current ? 'text-gray-300' : 'text-gray-400 group-hover:text-gray-300', 'mr-4 flex-shrink-0 h-6 w-6']" aria-hidden="true" />
                                    {{ item.name }}
                                </a>
                            </nav>
                        </div>
                    </div>
                </TransitionChild>
                <div class="flex-shrink-0 w-14" aria-hidden="true" />
            </Dialog>
        </TransitionRoot>

        <div class="hidden md:flex md:w-80 md:flex-col md:fixed md:inset-y-0">
            <div class="flex-1 flex flex-col min-h-0 bg-slate-900">
                <div class="h-16 px-4 bg-slate-800 items-center flex pl-6">
                    <Link :href="route('home')">
                        <ApplicationLogo />
                    </Link>
                </div>
                <div class="flex-1 flex flex-col overflow-y-auto pt-5">
                    <nav class="flex-1 px-6 py-4 space-y-1">
                        <template v-for="item in navigation" :key="item.name">
                            <div v-if="!item.children">
                                <a :href="item.href" :class="[item.current ? 'bg-slate-800/40 text-indigo-300' : 'text-white hover:bg-slate-800/40', 'group flex items-center px-2 py-2 text-sm font-semibold rounded-md']">
                                    <component :is="item.icon" :class="[item.current ? 'text-indigo-500' : 'text-indigo-300/40', 'mr-3 flex-shrink-0 h-6 w-6']" aria-hidden="true" />
                                    {{ item.name }}
                                </a>
                            </div>
                            <Disclosure as="div" v-else class="space-y-1 w-full" v-slot="{ open }">
                                <DisclosureButton :class="[item.current ? 'bg-slate-800/40 text-indigo-500' : 'text-white hover:bg-slate-800/40', 'group flex items-center px-2 py-2 text-sm font-semibold rounded-md w-full justify-between transition-all ease-in-out']">
                                    <div class="flex items-center">
                                        <component :is="item.icon" :class="[item.current ? 'text-indigo-500' : 'text-indigo-300/40', 'mr-3 flex-shrink-0 h-6 w-6']" aria-hidden="true" />
                                        {{ item.name }}
                                    </div>
                                    <component :is="ChevronDownIcon" :class="[open ? 'rotate-180' : 'text-indigo-300/40', 'flex-shrink-0 h-5 w-5']" aria-hidden="true" />
                                </DisclosureButton>
                                <transition
                                    enter-active-class="transition ease-in-out duration-300 transform"
                                    enter-from-class="-translate-x-10"
                                    enter-to-class="translate-x-0"
                                    leave-active-class="transition ease-in-out duration-300 transform"
                                    leave-from-class="translate-x-0"
                                    leave-to-class="-translate-x-10"
                                >
                                    <DisclosurePanel class="space-y-1">
                                        <DisclosureButton v-for="subItem in item.children" :key="subItem.name" as="a" :href="subItem.href" class="group w-full flex items-center pl-11 pr-2 py-2 text-sm font-semibold text-gray-400 rounded-md hover:text-white transition-all">
                                            {{ subItem.name }}
                                        </DisclosureButton>
                                    </DisclosurePanel>
                                </transition>
                            </Disclosure>
                        </template>
                    </nav>

                </div>
            </div>
        </div>
        <div class="md:pl-80 flex flex-col">
            <div class="sticky top-0 z-10 flex-shrink-0 flex h-16 bg-slate-800 shadow">
                <button type="button" class="px-4 border-r border-gray-200 text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500 md:hidden" @click="sidebarOpen = true">
                    <span class="sr-only">Open sidebar</span>
                    <Bars3Icon class="h-6 w-6" aria-hidden="true" />
                </button>
                <div class="flex-1 px-4 flex justify-end my-auto">
                    <div>
                        <form class="w-full flex md:ml-0 " action="#" method="GET">
                            <label for="search-field" class="sr-only">Search</label>
                            <div class="relative w-full text-gray-400 focus-within:text-gray-600">
                                <div class="absolute inset-y-0 left-0 flex items-center pointer-events-none">
                                    <MagnifyingGlassCircleIcon class="h-5 w-5" aria-hidden="true" />
                                </div>
                                <input id="search-field" class="bg-slate-700 rounded-lg block w-full h-full pl-8 pr-3 py-2 border-transparent text-gray-900 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 focus:ring-0 focus:border-transparent sm:text-sm" placeholder="Search" type="search" name="search" />
                            </div>
                        </form>
                    </div>
                    <div class="ml-4 flex items-center md:ml-6">
                        <button type="button" class="bg-slate-800 p-1 rounded-full text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                            <span class="sr-only">View notifications</span>
                            <BellIcon class="h-6 w-6" aria-hidden="true" />
                        </button>

                        <!-- Profile dropdown -->
                        <Menu as="div" class="ml-3 relative">
                            <div>
                                <MenuButton class="max-w-xs bg-white flex items-center text-sm rounded-full focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                                    <span class="sr-only">Open user menu</span>
                                    <img class="h-8 w-8 rounded-full" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="" />
                                </MenuButton>
                            </div>
                            <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                                <MenuItems class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
                                    <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }">
                                        <a :href="item.href" :class="[active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm text-gray-700']">{{ item.name }}</a>
                                    </MenuItem>
                                </MenuItems>
                            </transition>
                        </Menu>
                    </div>
                </div>
            </div>
            <main class="flex-1">
                <div class="py-8">
                    <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8 pb-5" v-if="$slots.header">
                        <slot name="header" />
                    </div>
                    <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
                        <slot />
                    </div>
                </div>
            </main>
        </div>
    </div>
</template>
