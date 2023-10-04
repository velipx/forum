<script setup>
import AdminLayout from '@/Layouts/AdminLayout.vue';
import ApplicationLogo from "@/Components/ApplicationLogo.vue";
import { DocumentIcon } from '@heroicons/vue/24/outline';
</script>

<template>
    <Head title="Forum" />

    <AdminLayout>
        <template #header>
            <h2 class="font-bold text-2xl text-white leading-tight">Dashboard</h2>
        </template>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
            <div class="col-1">
                <section class="rounded-xl bg-white shadow-sm dark:bg-slate-800">
                    <div class="p-6">
                        <div class="flex items-center gap-x-3">
                            <div
                                style="background-image: url('https://ui-avatars.com/api/?name=F+V&amp;color=FFFFFF&amp;background=a5b4fc');"
                                class="bg-cover bg-center h-10 w-10 rounded-full"></div>

                            <div class="flex-1">
                                <h2 class="grid flex-1 text-base font-semibold leading-6 text-gray-950 dark:text-white">
                                    Welcome back,
                                </h2>

                                <p class="text-sm text-gray-500 dark:text-slate-300">
                                    {{ $page.props.auth.user.name }}
                                </p>
                            </div>

                            <Link
                                class="relative grid-flow-col items-center justify-center font-semibold outline-none transition duration-75 focus:ring-2 rounded-lg gap-1.5 px-3 py-2 text-sm inline-grid shadow-sm bg-white text-gray-950 hover:bg-gray-50 dark:bg-slate-600 dark:text-white dark:hover:bg-slate-500"
                                type="submit"
                                :href="route('logout')" method="post" as="button">

                                <span>
                                    Sign out
                                </span>
                            </Link>
                        </div>
                    </div>
                </section>
            </div>
            <div class="col-1">
                <section class="rounded-xl bg-white shadow-sm dark:bg-slate-800">
                    <div class="p-5">
                        <div class="flex items-center gap-x-3">
                            <div class="flex-1">
                               <ApplicationLogo h="8" />

                                <p class="mt-1 text-xs text-gray-500 dark:text-gray-400">
                                    {{ $page.props.version }}
                                </p>
                            </div>

                            <div class="flex flex-col items-end gap-y-1">
                                <a href="#" target="_blank"
                                   class="relative inline-flex items-center justify-center font-semibold outline-none transition duration-75 hover:underline focus:underline gap-1.5 text-sm text-gray-700 dark:text-gray-200"
                                >
                                    <DocumentIcon class="h-5 w-5 text-gray-400 dark:text-slate-500" />
                                    Documentation
                                </a>

                                <a href="https://github.com/velipx/forum" target="_blank"
                                   class="relative inline-flex items-center justify-center font-semibold outline-none transition duration-75 hover:underline focus:underline gap-1.5 text-sm text-gray-700 dark:text-gray-200"
                                >
                                    <div class="h-5 w-5 text-gray-400 dark:text-slate-500">
                                        <svg viewBox="0 0 98 96" xmlns="http://www.w3.org/2000/svg">
                                            <path clip-rule="evenodd" fill="currentColor" fill-rule="evenodd"
                                                  d="M48.854 0C21.839 0 0 22 0 49.217c0 21.756 13.993 40.172 33.405 46.69 2.427.49 3.316-1.059 3.316-2.362 0-1.141-.08-5.052-.08-9.127-13.59 2.934-16.42-5.867-16.42-5.867-2.184-5.704-5.42-7.17-5.42-7.17-4.448-3.015.324-3.015.324-3.015 4.934.326 7.523 5.052 7.523 5.052 4.367 7.496 11.404 5.378 14.235 4.074.404-3.178 1.699-5.378 3.074-6.6-10.839-1.141-22.243-5.378-22.243-24.283 0-5.378 1.94-9.778 5.014-13.2-.485-1.222-2.184-6.275.486-13.038 0 0 4.125-1.304 13.426 5.052a46.97 46.97 0 0 1 12.214-1.63c4.125 0 8.33.571 12.213 1.63 9.302-6.356 13.427-5.052 13.427-5.052 2.67 6.763.97 11.816.485 13.038 3.155 3.422 5.015 7.822 5.015 13.2 0 18.905-11.404 23.06-22.324 24.283 1.78 1.548 3.316 4.481 3.316 9.126 0 6.6-.08 11.897-.08 13.526 0 1.304.89 2.853 3.316 2.364 19.412-6.52 33.405-24.935 33.405-46.691C97.707 22 75.788 0 48.854 0z"></path>
                                        </svg>
                                    </div>

                                    Github
                                </a>
                            </div>
                        </div>
                    </div>
                </section>
            </div>
        </div>
    </AdminLayout>
</template>