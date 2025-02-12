<template>
    <div class="flex flex-col text-center mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="gap-6 flex flex-wrap justify-center">
        <a v-for="{ href, icon, title, name } in btns" :href="href" target="_blank" rel="noopener noreferrer"
            class="bg-white inline-flex shadow-md rounded h-16 w-44 items-center justify-start gap-2 whitespace-nowrap border border-slate-900 px-3.5 text-base text-slate-900 font-semibold tracking-wide">
            <icon :icon="icon" class="size-10"></icon>
            <span class="flex flex-col">
                <span class="text-xs font-normal">{{ title }}</span>
                <span>{{ name }}</span>
            </span>
        </a>
    </div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];
const btns = [{
    name: "run.vues3.ru",
    title: "Open web app",
    href: "https://run.vues3.ru",
    icon: "mdi:web"
}, {
    name: "Windows",
    title: "Get exe for",
    href: "https://github.com/vues3/vues3/releases/latest",
    icon: "logos:microsoft-windows-icon"
}, {
    name: "macOS",
    title: "Get dmg for",
    href: "https://github.com/vues3/vues3/releases/latest",
    icon: "logos:apple"
}, {
    name: "Linux",
    title: "Get AppImage for",
    href: "https://github.com/vues3/vues3/releases/latest",
    icon: "logos:linux-tux"
}, {
    name: "Linux",
    title: "Get snap for",
    href: "https://snapcraft.io/vues3",
    icon: "vscode-icons:file-type-snapcraft"
}];
</script>
