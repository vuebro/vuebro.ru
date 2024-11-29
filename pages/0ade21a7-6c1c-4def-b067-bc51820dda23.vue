<template>
    <div class="flex items-center bg-cover bg-center min-h-[66dvh]"
        :style="`background-image:url(${the.images[0].url})`" un-cloak>
        <div class="container mx-auto px-4 py-12 place-items-center grid">
            <div
                class="gap-4 flex items-center justify-around w-full flex-col lg:flex-row-reverse bg-black/20 rounded-3xl shadow-2xl pa-6 backdrop-blur-sm bg-clip-border border-2 border-white/80">
                <img src="images/vues3.svg" class="w-36 lg:w-48 rounded-full lg:ma-10" decoding="async">
                <div class="text-center lg:text-left text-xs sm:text-sm md:text-base">
                    <h3 class="text-2xl lg:text-3xl text-slate-50 mb-6 font-['Rubik_Mono_One'] drop-shadow">{{
                        visible
                        }}<span class="blink underline decoration-white decoration-4 text-transparent">{{ title[length]
                            }}</span><span class="invisible">{{ invisible }}</span>
                    </h3>
                    <el-text size="large" class="!text-slate-50 drop-shadow" tag="b">{{ the.description }}</el-text>
                </div>
            </div>
        </div>
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
</style>
