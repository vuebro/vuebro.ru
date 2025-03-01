<template>
    <div class="container mx-auto" un-cloak>
        <div class="gap-4 flex items-center justify-around w-full flex-col lg:flex-row-reverse pa-6 text-slate-700">
            <img src="images/vues3.svg" class="w-36 lg:w-48 rounded-full ma-10 drop-shadow-2xl" decoding="async">
            <div class="text-center !lg:text-left text-xs sm:text-sm md:text-base">
                <h3 class="text-4xl lg:text-5xl mb-6 font-['Kelly_Slab']">{{
                    visible
                    }}<span
                        class="blink underline decoration-slate-700 decoration-3 lg:decoration-4 text-transparent">{{
                            typewriter[length]
                        }}</span><span class="invisible">{{ invisible }}</span>
                </h3>
                <el-text size="large" type="info">{{ the.description }}</el-text>
            </div>
        </div>
        <div class="gap-6 flex flex-wrap justify-center">
            <a v-for="{ href, icn, title, name } in btns" :href="href" target="_blank" rel="noopener noreferrer"
                class="bg-white inline-flex shadow-md rounded h-16 w-44 items-center justify-start gap-2 whitespace-nowrap border border-slate-900 px-3.5 text-base text-slate-900 font-semibold tracking-wide">
                <icon :icon="icn" class="size-10"></icon>
                <span class="flex flex-col">
                    <span class="text-xs font-normal">{{ title }}</span>
                    <span>{{ name }}</span>
                </span>
            </a>
        </div>
        <div class="justify-center flex flex-wrap gap-2 my-24">
            <span v-if="title">
                <el-button size="large" type="primary" round :to="to" tag="router-link" class="w-48">
                    <icon :icon="startIcon" class="size-6 mr-1"></icon>
                    {{ title }}
                    <el-icon class="el-icon--right">
                        <ArrowRight />
                    </el-icon>
                </el-button>
            </span>
            <span v-for="{ brandIcon, text, link } in social">
                <el-button tag="a" :href="link" target="_blank" size="large" type="plain" round class="w-48">
                    <icon :icon="brandIcon" class="size-6 mr-1"></icon>
                    {{ text }}
                    <el-icon class="el-icon--right">
                        <ArrowRight />
                    </el-icon>
                </el-button>
            </span>
        </div>
    </div>
    <div class="absolute -z-10 inset-0 m-auto max-w-xs h-[357px] blur-[118px] sm:max-w-md md:max-w-lg bg-gradient"
        un-cloak>
    </div>
</template>

<script setup>
import { inject, ref, computed } from "vue";
import { ArrowRight } from "@element-plus/icons-vue";

const { id } = defineProps(["id"]),
    the = inject("pages")[id],
    { $children: [{ title, to, icon: startIcon } = {}] = [] } = Object.values(inject("pages")).find(({ name }) => name === "документация") ?? {};

const typewriter = `${the.title}_`,
    index = ref(0),
    length = computed(() => {
        const count = Math.floor(index.value / typewriter.length);
        return count % 2 ? typewriter.length - 1 : index.value - count * typewriter.length;
    }),
    visible = computed(() => typewriter.substring(0, length.value)),
    invisible = computed(() => typewriter.substring(length.value + 1));

const btns = [{
    name: "www",
    title: "Open web app",
    href: "https://run.vues3.ru",
    icn: "mdi:web"
}, {
    name: "Windows",
    title: "Get exe for",
    href: "https://github.com/vues3/vues3/releases/latest",
    icn: "logos:microsoft-windows-icon"
}, {
    name: "macOS",
    title: "Get dmg for",
    href: "https://github.com/vues3/vues3/releases/latest",
    icn: "logos:apple"
}, {
    name: "Linux",
    title: "Get AppImage for",
    href: "https://github.com/vues3/vues3/releases/latest",
    icn: "logos:linux-tux"
}, {
    name: "Linux",
    title: "Get snap for",
    href: "https://snapcraft.io/vues3",
    icn: "vscode-icons:file-type-snapcraft"
}],
    social = [
        { brandIcon: "fa6-brands:github", text: "vueS3 на github", link: "https://github.com/vues3" },
        { brandIcon: "fa6-brands:vk", text: "vueS3 вконтакте", link: "https://vk.com/vues3" }
    ];

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
