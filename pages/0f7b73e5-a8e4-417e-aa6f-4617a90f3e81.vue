<template>
    <el-carousel type="card" :height="Height" indicator-position="outside" un-cloak>
        <el-carousel-item v-for="i in 6" class="!h-auto" v-element-size="elementSise"><img
                :src="`images/screenshots/${i}.png`" decoding="async"></el-carousel-item>
    </el-carousel>
</template>

<script setup>
import { ref, watch, onMounted } from "vue";
import { useRoute } from "vue-router";
import { vElementSize } from "@vueuse/components";

const route = useRoute(),
    Height = ref(""),
    elementSise = async ({ height }) => {
        if (height) requestAnimationFrame(() => { Height.value = `${height}px`; });
    };

onMounted(() => {
    const element = document.getElementById(String(route.name));
    watch(Height, () => { element.scrollIntoView({ behavior: "smooth" }) }, { once: true, flush: "post" });
});
</script>