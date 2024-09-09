<script lang="ts" setup>
const navLinks = ref<{
    to: string,
    label: string
}[]>([
    {
        to: "/",
        label: "Home",
    },
    {
        to: "/",
        label: "About",
    },
    {
        to: "/",
        label: "Contact",
    }
])
</script>

<template>
    <div class="fixed top-0 left-0 right-0 border-b border-white/20 bg-blur">
        <nav class="container py-4 flex justify-between ">
            <NuxtLink :to="{
                name: 'index',
            }" class="text-2xl font-bold text-white">SnipURL</NuxtLink>
            <ul class="flex items-center gap-4">
            <li v-for="navLink in navLinks" :key="navLink.to"><NuxtLink :to="navLink.to">{{ navLink.label }}</NuxtLink></li>
            <li class="btn btn-primary"><NuxtLink to="/auth">Sign In</NuxtLink></li>
        </ul>
        </nav>
    </div> 
</template>