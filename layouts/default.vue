<template >
    <header class="flex flex-row w-full shadow-lg shadow-gray-400 max-sm:relative max-sm:justify-between">
        <div class="basis-1/4 items-center justify-start px-4 max-sm:basis-auto">
            <img src="assets/images/icon.png" class=" h-20" alt="Logo">
        </div>
        
        <nav :class="burger 
            ? 'basis-1/2 flex flex-col absolute top-full left-0 w-full bg-white px-0 max-sm:flex'
            : 'basis-1/2 flex flex-row items-center justify-end px-8 gap-4 max-sm:hidden'">
            <NuxtLink to="/" class="p-2 hover:bg-gray-500 rounded-lg max-sm:border-b-2 max-sm:w-full max-sm:border-black max-sm:text-center">Home</NuxtLink>
            
            <div class="relative">
                <div class="p-2 cursor-pointer hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:text-center" @click="switch_submenu">LABS</div>
                <div v-show="submenu" class="absolute left-0 top-full w-full bg-white shadow-md max-sm:relative">
                    <NuxtLink to="/lab4" class="block p-2 border-b hover:bg-gray-500 hover:text-white">LAB4</NuxtLink>
                    <NuxtLink to="/lab5" class="block p-2 border-b hover:bg-gray-500 hover:text-white">LAB5</NuxtLink>
                    <NuxtLink to="/lab6" class="block p-2 border-b hover:bg-gray-500 hover:text-white">LAB6</NuxtLink>
                </div>
            </div>

            <NuxtLink to="/login" class="p-2 hover:bg-gray-500 rounded-lg max-sm:border-b-2 max-sm:w-full max-sm:border-black max-sm:text-center">Login</NuxtLink>
            <NuxtLink to="/logout" class="p-2 hover:bg-gray-500 rounded-lg max-sm:border-b-2 max-sm:w-full max-sm:border-black max-sm:text-center">Logout</NuxtLink>
        </nav>

        <!-- Кнопка бургера -->
        <div @click="switch_burger" class="max-sm:flex flex-col justify-center items-center space-y-1 p-2 cursor-pointer">
            <span class="h-[3px] w-6 bg-gray-700 transition-transform" :class="burger ? 'rotate-45 translate-y-[6px]' : ''"></span>
            <span class="h-[3px] w-6 bg-gray-700 transition-opacity" :class="burger ? 'opacity-0' : ''"></span>
            <span class="h-[3px] w-6 bg-gray-700 transition-transform" :class="burger ? '-rotate-45 -translate-y-[6px]' : ''"></span>
        </div>
    </header>

    <main class=" flex bg-gray-300">
        <slot />
    </main>

    <footer class="flex flex-row bg-gray-75 border-t-2 border-gray-100 items-center justify-center px-6 py-2 gap-3">
        <a href="https://www.youtube.com/" class="hover:sepia hover:brightness-125 hover:contrast-150"><img src="assets/images/youtube.svg" class="h-16 w-16" alt="YouTube"></a>
        <a href="https://github.com/"><img src="assets/images/github.svg" class="h-16 w-16 transition duration-300 hover:grayscale" alt="GitHub"></a>
        <a href="https://www.facebook.com/"><img src="assets/images/facebook.svg" class="h-16 w-16" alt="Facebook"></a>
        <a href="https://steamcommunity.com/"><img src="assets/images/steam.svg" class="h-16 w-16" alt="Steam"></a>
    </footer>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { useHead } from '#app';

useHead({
    script: [
        {
            async: true,
            src: 'https://www.googletagmanager.com/gtag/js?id=G-GMRMMGH1FY'
        },
        {
            innerHTML: `
            window.dataLayer = window.dataLayer || [];
            function gtag(){dataLayer.push(arguments);}
            gtag('js', new Date());
            gtag('config', 'G-GMRMMGH1FY');
            `,
            type: 'text/javascript',
        },
    ],
    _dangerouslyDisableSanitizersByTagID: {
        gtag: ['innerHTML'],
    },
});

const burger = ref<boolean>(false);
const submenu = ref<boolean>(false);

const switch_burger = () => {
    burger.value = !burger.value;
    if (!burger.value) submenu.value = false; // Закрываем подменю при закрытии бургера
};

const switch_submenu = () => {
    submenu.value = !submenu.value;
};
</script>
