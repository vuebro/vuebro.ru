<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <el-text>{{ t("site") }}: <a href="https://element-plus.org"
                target="_blank">https://element-plus.org</a></el-text>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Importmap</h3>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit not-prose">
            <template v-for="{ key, value } in params">
                <dt class="font-bold text-slate-700">{{ key }}</dt>
                <dd class="text-slate-500 overflow-hidden text-ellipsis">{{ value }}</dd>
            </template>
        </dl>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">{{ t("code") }}</h3>
        <highlightjs language="js" :code="js" class="not-prose"></highlightjs>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">{{ t("example") }}</h3>
        <el-tabs class="not-prose 2xl:row-start-auto">
            <el-tab-pane :label="t('result')">
                <el-card class="ma-4 max-w-96">
                    <template #header>Yummy hamburger</template>
                    <el-image
                        src="https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png"
                        class="w-full h-52" fit="cover"></el-image>
                </el-card>
            </el-tab-pane>
            <el-tab-pane label="Template">
                <highlightjs language="html" :code="html"></highlightjs>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script setup vapor>
import { ElImage } from "element-plus";
import { inject } from "vue";
import { useI18n } from "vue-i18n";

const { t } = useI18n({
    messages: {
        en: {
            site: "The project website",
            example: "An example of usage",
            result: "Result",
            code: "The code for connecting a library"
        },
        ru: {
            site: "Сайт проекта",
            example: "Пример использования",
            result: "Результат",
            code: "Код для подключения библиотеки"
        }
    }
}),
    { pid } = defineProps(["pid"]),
    the = inject("pages")[pid],
    params = [{
        key: "element-plus",
        value: "https://cdn.jsdelivr.net/npm/element-plus@2/dist/index.full.min.mjs"
    }],
    js = `<script setup>
import { getCurrentInstance } from "vue";
import ElementPlus from "element-plus";
const { appContext: { app } } = getCurrentInstance();
app.use(ElementPlus);
<\/script>

<style>
@import "https://cdn.jsdelivr.net/npm/element-plus@2/dist/index.css";
</style>`,
    html = `<el-card class="ma-4 max-w-96">
    <template #header>Yummy hamburger</template>
    <el-image
        src="https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png"
        class="w-full h-52" fit="cover"></el-image>
</el-card>`;
</script>
