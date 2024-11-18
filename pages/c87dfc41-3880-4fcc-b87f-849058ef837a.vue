<template>
<div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="not-prose gap-6 flex flex-wrap justify-around">
        <template v-for="{icon, to, enabled, title} in the.children">
            <router-link :to="to" v-if="enabled" class="items-center text-center flex flex-col">
                <icon :icon="icon" class="size-24 ma-6"></icon>
                <el-text tag="b">{{ title }}</el-text>
            </router-link>
            <div v-else class="items-center text-center flex flex-col">
                <div :class="i" class="size-24 ma-6 text-slate-400"></div>
                <el-text tag="b">{{ title }}</el-text>
            </div>
        </template>
    </div>
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

</script>


