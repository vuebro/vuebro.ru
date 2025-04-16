<template>
    <div class="min-h-dvh" un-cloak>
        <div class="sticky top-0 z-50 pa-4 border-b bg-neutral-50 opacity-0 md:hover:opacity-100 transition-opacity duration-1000"
            :class="{ 'opacity-100': !ready }" ref="pageHeader">
            <el-page-header icon="" :content="pages[$route.name].title">
                <template #breadcrumb>
                    <el-breadcrumb separator="/">
                        <el-breadcrumb-item v-for="item in pages[$route.name].branch" :to="item.to">
                            {{ item.name }}
                        </el-breadcrumb-item>
                    </el-breadcrumb>
                </template>
                <template #title>
                    <router-link to="/" class="whitespace-nowrap flex items-center max-sm:hidden">
                        <el-avatar src="images/vues3.svg" size="small"></el-avatar>
                    </router-link>
                </template>
                <template #extra>
                    <el-button circle @click="drawer = true">
                        <icon icon="mdi:menu" class="size-5"></icon>
                    </el-button>
                </template>
            </el-page-header>
        </div>
        <router-view></router-view>
    </div>
    <footer class="text-slate-500 mt-24" un-cloak>
        <div class="pt-16 pb-12 text-sm border-t border-slate-200 bg-slate-100">
            <div class="container px-6 mx-auto">
                <div class="grid grid-cols-4 md:grid-cols-8 lg:grid-cols-12 gap-6">
                    <div class="col-span-4 md:col-span-8 lg:col-span-4 mb-3">
                        <img class="-mt-16 w-full md:w-60 max-md:max-w-60 mx-auto" src="images/drakkar.svg"
                            decoding="async">
                        <h4 class="text-center text-base text-slate-700 font-medium">{{ t("madeof") }}</h4>
                    </div>
                    <nav class="col-span-2 md:col-span-4 lg:col-span-2" v-for="{ name, children, icon } in views">
                        <h3 class="mb-6 text-base text-slate-700 font-medium whitespace-nowrap">
                            <icon :icon="icon" class="mr-2 size-8 inline"></icon>{{ name }}
                        </h3>
                        <ul>
                            <li v-for="child in children" class="mb-2 leading-6">
                                <router-link :to="child.to" v-if="child?.enabled"
                                    class="transition-colors duration-300 hover:text-emerald-500 focus:text-emerald-600">
                                    <icon :icon="child.icon" class="mr-2 size-6 inline"></icon>{{ child.name }}
                                </router-link>
                            </li>
                        </ul>
                    </nav>
                </div>
            </div>
        </div>
        <div class="py-4 text-sm border-t border-slate-200 bg-slate-100">
            <div class="container px-6 mx-auto">
                <div class="flex flex-col md:flex-row w-full gap-4 justify-between">
                    <div class="flex items-center col-span-1 gap-4 text-base font-medium leading-6"><img
                            class="size-6 shrink-0" src="images/vues3.svg">{{ the.description }}
                    </div>
                    <nav class="text-right col-span-2 md:col-span-4 lg:col-span-6">
                        <ul class="flex items-center justify-end gap-4">
                            <li v-for="{ icon, href } in social">
                                <a :href="href" target="_blank" rel="noopener noreferrer"
                                    class="transition-colors duration-300 hover:text-sky-600 focus:text-sky-700">
                                    <icon class="size-6 shrink-0" :icon="icon"></icon>
                                </a>
                            </li>
                        </ul>
                    </nav>
                </div>
            </div>
        </div>
    </footer>
    <div id="drawer" un-cloak>
        <el-drawer v-model="drawer" :title="the.header" class="w-full sm:w-96" size="">
            <el-menu :router="true" :default-openeds="[0, 1, 2]">
                <el-sub-menu v-for="({ name, $children, icon }, index) in views" :index="index">
                    <template #title>
                        <icon :icon="icon" class="icon"></icon><span>{{ name }}</span>
                    </template>
                    <el-menu-item v-for="(child, index2) in $children" :route="{ name: child.id }" :index="index2">
                        <icon :icon="child.icon" class="icon"></icon><span>{{ child.name }}</span>
                    </el-menu-item>
                </el-sub-menu>
            </el-menu>
        </el-drawer>
    </div>
    <el-backtop></el-backtop>
</template>
<script setup>
import "./node_modules/@highlightjs/cdn-assets/styles/stackoverflow-light.min.css";
import "./node_modules/element-plus/dist/index.css";
import "./node_modules/animate.css/animate.min.css";
import { createVuetify, components, directives } from "vuetify";
import { useRoute } from "vue-router";
import { Quasar } from "quasar";
import { computed, ref, inject, useTemplateRef, onMounted, watch } from "vue";
import { get, set } from "@vueuse/core";
import { createI18n, useI18n } from "vue-i18n";
import ElementPlus from "element-plus";
import { Icon } from '@iconify/vue';
import hljs from "highlight.js/lib/core";
import javascript from "highlight.js/lib/languages/javascript";
import css from "highlight.js/lib/languages/css";
import xml from "highlight.js/lib/languages/xml";
import hljsVuePlugin from "@highlightjs/vue-plugin";
hljs.default.registerLanguage("javascript", javascript.default);
hljs.default.registerLanguage("css", css.default);
hljs.default.registerLanguage("xml", xml.default);
window.app.use(createVuetify({ components, directives }));
window.app.component("Icon", Icon);
window.app.use(createI18n({ legacy: false, locale: "ru", fallbackLocale: "en" }))
window.app.use(ElementPlus);
window.app.use(Quasar);
window.app.use(hljsVuePlugin.default);
const { t } = useI18n({
    messages: {
        en: {
            madeof: "Made on the shores of the Baltic Sea",
            socialUrl: "https://facebook.com/vues3",
            socialIcon: "fa-brands:facebook"
        },
        ru: {
            madeof: "Сделано на берегах Балтики",
            socialUrl: "https://vk.com/vues3",
            socialIcon: "fa-brands:vk"
        }
    }
});
const { id } = defineProps(["id"]),
    pages = inject("pages"),
    the = pages[id],
    views = computed(() => the.$children.filter(({ $children }) => $children.length)),
    ready = ref(true),
    pageHeaderRef = useTemplateRef("pageHeader"),
    drawer = ref(false),
    route = useRoute(),
    social = [{
        icon: "fa-brands:github",
        href: "https://github.com/vues3"
    }, {
        icon: t("socialIcon"),
        href: t("socialUrl")
    }];
onMounted(() => {
    let timeoutID;
    const scroll = () => {
        set(ready, false);
        if (timeoutID) clearTimeout(timeoutID);
        if (window.scrollY > get(pageHeaderRef, "offsetHeight")) timeoutID = setTimeout(() => {
            set(ready, true);
        }, 2000);
    };
    document.addEventListener("scroll", scroll);
    scroll();
});
watch(() => route.name, () => { drawer.value = false });
</script>
<style scoped>
.el-drawer .el-menu {
    border-right: none;
}

#drawer :deep(.el-drawer__body) {
    padding: 0;
}

.icon {
    margin-right: 1rem;
    width: 2rem;
    height: 2rem;
}
</style>
