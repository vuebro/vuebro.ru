<template>
    <el-carousel type="card" :height="height" indicator-position="outside" un-cloak>
        <el-carousel-item v-for="({ alt, url }, i) in images" class="!h-fit"
            v-element-size="({ height }) => { heights[i] = height }"><img :src="url" :alt="alt"
                decoding="async"></el-carousel-item>
    </el-carousel>
</template>

<script setup>
import { inject, ref, watch } from "vue";
import { vElementSize } from "@vueuse/components";
import { set } from "@vueuse/core";

const { id } = defineProps(["id"]),
    { images } = inject("pages")[id],
    heights = ref([]),
    height = ref(""),
    deep = true;

watch(heights, (value) => { requestAnimationFrame(() => { set(height, `${Math.max(...value)}px`) }) }, { deep });
</script>