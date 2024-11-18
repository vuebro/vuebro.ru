<template>
<div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-12">
        <el-image v-for="(src, index) in urls" :src="src" :preview-src-list="urls" :initial-index="index"
            class="shadow-md rounded hover:shadow-2xl"></el-image>
    </div>
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];
const urls = [
    "images/screenshots/screenshot_1.png",
    "images/screenshots/screenshot_2.png",
    "images/screenshots/screenshot_3.png",
    "images/screenshots/screenshot_4.png",
    "images/screenshots/screenshot_5.png",
];
</script>


