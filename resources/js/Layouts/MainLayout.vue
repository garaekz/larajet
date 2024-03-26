<script setup>
import { Head } from '@inertiajs/vue3';
import SideMenu from '@/Components/Main/SideMenu.vue';
import TopMenu from '@/Components/Main/TopMenu.vue';

defineProps({
    title: String,
});
</script>

<template>
    <div class="grid min-h-screen w-full md:grid-cols-[220px_1fr] lg:grid-cols-[280px_1fr]">

        <Head :title="title" />
        <SideMenu />
        <div class="flex flex-col">
            <TopMenu :user="$page.props.auth.user" />
            <main class="flex flex-1 flex-col gap-4 p-4 lg:gap-6 lg:p-6">
                <slot name="header" />
                <slot />
            </main>
        </div>
    </div>
</template>