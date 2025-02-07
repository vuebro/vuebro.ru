<template>
    <div class="container mx-auto gap-4 flex items-center justify-around w-full flex-col lg:flex-row-reverse pa-6 text-slate-700"
        un-cloak>
        <img src="images/vues3.svg" class="w-36 lg:w-48 rounded-full ma-10 drop-shadow-2xl" decoding="async">
        <div class="text-center lg:text-left text-xs sm:text-sm md:text-base">
            <h3 class="text-4xl lg:text-5xl mb-6 font-['Kelly_Slab']">{{
                visible
                }}<span class="blink underline decoration-slate-700 decoration-3 lg:decoration-4 text-transparent">{{
                    title[length]
                    }}</span><span class="invisible">{{ invisible }}</span>
            </h3>
            <el-text size="large" type="info">{{ the.description }}</el-text>
        </div>
    </div>
    <div class="absolute -z-10 inset-0 m-auto max-w-xs h-[357px] blur-[118px] sm:max-w-md md:max-w-lg bg-gradient">
    </div>
</template>

<script setup>
import { inject, ref, computed } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const title = `${the.title}_`;

const index = ref(0);

const length = computed(() => {
    const count = Math.floor(index.value / title.length);
    return count % 2 ? title.length - 1 : index.value - count * title.length;
});

const visible = computed(() => title.substring(0, length.value));
const invisible = computed(() => title.substring(length.value + 1));

setInterval(() => { index.value += 1; }, 200);
</script>

<style scoped>
.blink {
    animation: blinker 1s step-start infinite;
}

@keyframes blinker {
    50% {
        opacity: 0;
    }
}

.bg-gradient {
    background: linear-gradient(106.89deg,
            rgba(192, 132, 252, 0.11) 15.73%,
            rgba(14, 165, 233, 0.41) 15.74%,
            rgba(232, 121, 249, 0.26) 56.49%,
            rgba(79, 70, 229, 0.4) 115.91%);
}
</style>
