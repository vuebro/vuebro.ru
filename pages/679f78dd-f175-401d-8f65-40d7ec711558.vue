<template>
<div class="container mx-auto px-4">
    <div class="flex flex-col text-center not-prose mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <el-text>Сайт проекта:</el-text> <el-link href="https://element-plus.org"
        target="_blank">https://element-plus.org</el-link>
    <h3>Importmap</h3>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
        <template v-for="{ key, value } in params">
            <dt class="font-bold text-slate-700">{{ key }}</dt>
            <dd class="text-slate-500">{{ value }}</dd>
        </template>
    </dl>
    <h3>Код для подключения библиотеки</h3>
    <highlightjs language="js" :code="js" class="not-prose"></highlightjs>
    <h3>Пример использования</h3>
    <el-tabs class="not-prose 2xl:row-start-auto">
        <el-tab-pane label="Template">
            <highlightjs language="html" :code="html"></highlightjs>
        </el-tab-pane>
        <el-tab-pane label="Результат">
            <el-alert title="Success alert" type="success" :closable="false" show-icon />
            <el-alert title="Info alert" type="info" :closable="false" show-icon />
            <el-alert title="Warning alert" type="warning" :closable="false" show-icon />
            <el-alert title="Error alert" type="error" :closable="false" show-icon />
        </el-tab-pane>
    </el-tabs>
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const params = [{
    key: "element-plus",
    value: "https://unpkg.com/element-plus/dist/index.full.min.mjs"
}];
const js = `import ElementPlus from "element-plus";
import "https://unpkg.com/element-plus/dist/index.css";
window.app.use(ElementPlus.default);`;
const html = `<el-alert title="Success alert" type="success" :closable="false" show-icon />
<el-alert title="Info alert" type="info" :closable="false" show-icon />
<el-alert title="Warning alert" type="warning" :closable="false" show-icon />
<el-alert title="Error alert" type="error" :closable="false" show-icon />`;
</script>


