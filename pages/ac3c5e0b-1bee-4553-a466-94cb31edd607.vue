<template>
    <div class="flex flex-col text-center not-prose mb-12" un-cloak>
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="not-prose gap-6 flex flex-wrap justify-around" un-cloak>
        <template v-for="({ icon, to, title }, index) in the.$children">
            <router-link :to="to"
                class="items-center text-center flex flex-col transition hover:drop-shadow-2xl animate__animated"
                v-intersection-observer="([{ isIntersecting }]) => { anima[index] = isIntersecting }"
                :class="[{ animate__flip: anima[index] }, `animate__delay-${index}s`]">
                <icon :icon="icon" class="size-24 ma-6"></icon>
                <el-text tag="b">{{ title }}</el-text>
            </router-link>
        </template>
    </div>
</template>

<script setup vapor>
import { inject, ref } from "vue";
import { vIntersectionObserver } from "@vueuse/components";
const { id } = defineProps(["id"]),
    the = inject("pages")[id],
    anima = ref([]);
</script>

<style>
:root {
  --animate-delay: 0.2s;
}
</style>