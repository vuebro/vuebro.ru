<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <el-text>{{ t("site") }}: <a href="https://vueuse.org" target="_blank">https://vueuse.org</a></el-text>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Importmap</h3>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit not-prose">
            <template v-for="{ key, value } in params">
                <dt class="font-bold text-slate-700">{{ key }}</dt>
                <dd class="text-slate-500 overflow-hidden text-ellipsis">{{ value }}</dd>
            </template>
        </dl>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">{{ t("example") }}</h3>
        <el-tabs class="not-prose 2xl:row-start-auto">
            <el-tab-pane :label="t('result')">
                <div>Now: {{ now }}</div>
            </el-tab-pane>
            <el-tab-pane label="Template">
                <highlightjs language="html" :code="html"></highlightjs>
            </el-tab-pane>
            <el-tab-pane label="Script">
                <highlightjs language="js" :code="js"></highlightjs>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script setup vapor>
import { useNow } from "@vueuse/core";
import { inject } from "vue";
import { useI18n } from "vue-i18n";

const now = useNow();

const { t } = useI18n({
    messages: {
        en: {
            site: "The project website",
            example: "An example of usage",
            result: "Result"
        },
        ru: {
            site: "Сайт проекта",
            example: "Пример использования",
            result: "Результат"
        }
    }
}),
    { pid } = defineProps(["pid"]),
    the = inject("pages")[pid],
    params = [{
        key: "@vueuse/core",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/core@14/dist/index.js"
    }, {
        key: "@vueuse/shared",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/shared@14/dist/index.js"
    }],
    js = `import { useNow } from '@vueuse/core';

const now = useNow();`;
const html = "<div>Now: {{ now }}</div>";
</script>