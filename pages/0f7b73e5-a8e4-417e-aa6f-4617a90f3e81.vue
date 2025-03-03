<template>
    <el-carousel type="card" :height="height" indicator-position="outside" un-cloak>
        <el-carousel-item v-for="i in 6" class="!h-fit" v-element-size="({ height }) => { heights[i - 1] = height }"><img
                :src="`images/screenshots/${i}.png`" decoding="async"></el-carousel-item>
    </el-carousel>
</template>

<script setup>
import { ref, watch } from "vue";
import { vElementSize } from "@vueuse/components";
import { set } from "@vueuse/core";

const heights = ref([]),
    height = ref(""),
    deep = true;

watch(heights, (value) => { requestAnimationFrame(() => { set(height, `${Math.max(...value)}px`) }) }, { deep });
</script>