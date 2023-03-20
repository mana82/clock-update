<script setup>
import {Head, Link} from '@inertiajs/vue3';

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    laravelVersion: String,
    phpVersion: String,
});
</script>

<template>

    <div class="min-h-screen bg-gray-100 text-gray-800 antialiased px-4 py-6 flex flex-col justify-center sm:py-12">
        <div class="relative py-3 sm:max-w-xl mx-auto text-center">
            <span class="text-2xl font-light">Login or Register</span>
            <div class="relative mt-4 bg-white shadow-md sm:rounded-lg text-left">
                <div class="h-2 bg-indigo-400 rounded-t-md"></div>
                <div class="py-6 px-8">
                    <div>
                        <Link v-if="$page.props.auth.user" :href="route('dashboard')" class="text-sm hover:underline">
                            Dashboard
                        </Link>
                    </div>
                    <div class="flex justify-between items-baseline">
                        <Link :href="route('login')"
                              class="mt-4 bg-indigo-500 text-white py-2 px-6 rounded-lg w-64 text-center">Log in
                        </Link>
                    </div>
                    <div class="flex justify-between items-baseline">
                        <Link v-if="canRegister" :href="route('register')"
                              class="mt-4 bg-indigo-500 text-white py-2 px-6 rounded-lg w-64 text-center">Register
                        </Link>
                    </div>

                </div>
                <div class="ml-4 text-sm text-gray-500 dark:text-gray-400 text-center sm:ml-0">
                    Laravel v{{ laravelVersion }} (PHP v{{ phpVersion }})
                </div>
            </div>
        </div>
    </div>


</template>

<style>

</style>
