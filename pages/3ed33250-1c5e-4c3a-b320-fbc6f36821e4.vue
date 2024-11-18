<template>
<div class="container mx-auto px-4" un-cloak>
    <div class="justify-center flex flex-wrap gap-2 mb-12"><span><el-button size="large" type="primary" round
            :to="the.children[0].to" tag="router-link" class="w-48">{{ the.children[0].title
            }}<el-icon class="el-icon--right">
                <ArrowRight />
            </el-icon></el-button></span>
        <span v-for="{icon, text, link} in social"><el-button tag="a" :href="link" target="_blank" rel="noopener noreferrer" size="large" type="plain" round
             class="w-48">
            <icon :icon="icon" class="mr-1"></icon>{{ text }}<el-icon class="el-icon--right">
                <ArrowRight />
            </el-icon>
        </el-button></span>
    </div>
    <div class="flex flex-col mb-12 text-center">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="pa-4 shadow-md rounded-3xl border-t border-t-slate-100 bg-white">
        <ul class="divide-y divide-slate-100">
            <li v-for="{icon, title, to, description} in the.$children" :key="icon">
                <router-link :to="to" class="flex items-start gap-4 px-4 py-3 hover:bg-slate-50">
                    <div class="flex items-center text-emerald-500">
                        <icon :icon="icon" class="size-10"></icon>
                    </div>
                    <div
                        class="flex flex-col gap-0 min-h-[2rem] items-start justify-center w-full min-w-0 overflow-hidden">
                        <h4 class="w-full text-base truncate text-slate-700">{{ title }}</h4>
                        <p class="w-full text-sm text-slate-500">{{ description }}</p>
                    </div>
                    <icon class="size-5 transition-colors text-slate-500 hover:text-emerald-500"
                        icon="ion:open-outline">
                    </icon>
                </router-link>
            </li>
        </ul>
    </div>
</div>
</template>

<script setup>
import { ArrowRight } from "@element-plus/icons-vue";

import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const social = [
    { icon: "fa-brands:github", text: "vueS3 на github", link: "https://github.com/vues3" },
    { icon: "fa-brands:vk", text: "vueS3 вконтакте", link: "https://vk.com/vues3" },
    { icon: "fa-brands:facebook", text: "vueS3 на facebook", link: "https://facebook.com/vues3" }
];
</script>


