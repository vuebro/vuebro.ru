<template>
    <div class="flex flex-col text-center not-prose mb-12" un-cloak>
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="pa-4 shadow-md rounded-3xl border-t border-t-slate-100 bg-white">
        <ul class="divide-y divide-slate-100">
            <li v-for="{ icon, title, to, description } in the.$children" :key="icon">
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
</template>

<script setup vapor>
import { inject } from "vue";

const { id } = defineProps(["id"]),
    the = inject("pages")[id];
</script>
