<template>
    <el-carousel type="card" height="auto" indicator-position="outside" ref="carousel" un-cloak>
        <el-carousel-item v-for="src in srcList" class="!h-auto"><img :src="src"
                @click="showPreview = true"></el-carousel-item>
    </el-carousel>
    <el-image-viewer v-if="showPreview" :url-list="srcList" show-progress :initial-index="carousel.activeIndex"
        @close="showPreview = false"></el-image-viewer>
</template>

<script setup vapor>
import { ref } from "vue";

const carousel = ref(),
    showPreview = ref(false),
    srcList = [...Array(6).keys()].map((key) => `images/screenshots/${key + 1}.png`);
</script>