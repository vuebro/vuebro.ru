<template>
    <el-carousel type="card" :height="Height" indicator-position="outside" ref="carousel" un-cloak>
        <el-carousel-item v-for="i in srcList.length" v-element-size="elementSise" class="!h-auto"><img
                :src="srcList[i - 1]" @click="showPreview = true"></el-carousel-item>
    </el-carousel>
    <el-image-viewer v-if="showPreview" :url-list="srcList" show-progress :initial-index="carousel.activeIndex"
        @close="showPreview = false"></el-image-viewer>
</template>

<script setup vapor>
import { ref, watch } from "vue";
import { useRoute } from "vue-router";
import { vElementSize } from "@vueuse/components";

const { name } = useRoute(),
    Height = ref(""),
    carousel = ref(),
    showPreview = ref(false),
    element = document.getElementById(String(name)),
    srcList = [...Array(6).keys()].map((key) => `images/screenshots/${key + 1}.png`),
    elementSise = ({ height }) => { if (height) requestAnimationFrame(() => { Height.value = `${height}px` }) };
watch(Height, () => { element.scrollIntoView({ behavior: "smooth" }) }, { once: true, flush: "post" });
</script>