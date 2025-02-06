<template>
<div class="container mx-auto px-4">
    <div class="flex flex-col text-center not-prose mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <el-text>Сайт проекта:</el-text> <el-link href="https://vueuse.org" target="_blank">https://vueuse.org</el-link>
    <h3>Importmap</h3>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
        <template v-for="{ key, value } in params">
            <dt class="font-bold text-slate-700">{{ key }}</dt>
            <dd class="text-slate-500">{{ value }}</dd>
        </template>
    </dl>
    <h3>Пример использования</h3>
    <el-tabs class="not-prose 2xl:row-start-auto">
        <el-tab-pane label="Template">
            <highlightjs language="html" :code="html"></highlightjs>
        </el-tab-pane>
        <el-tab-pane label="Script">
            <highlightjs language="js" :code="js"></highlightjs>
        </el-tab-pane>
        <el-tab-pane label="Результат">
            <div class="grid grid-flow-col grid-gap-4 place-content-center place-items-center font-mono">
                <div class="font-mono bg-light-500 dark:bg-dark-500 flex flex-col text-center p-2 border-rounded">
                    <span class="text-4xl">{{ x }}</span>
                    <span class="text-sm dark:text-light-900 dark:text-opacity-50 mt-2">Mouse X</span>
                </div>
                <div class="font-mono bg-light-500 dark:bg-dark-500 flex flex-col text-center p-2 border-rounded">
                    <span class="text-4xl">{{ y }}</span>
                    <span class="text-sm dark:text-light-900 dark:text-opacity-50 mt-2">Mouse Y</span>
                </div>
            </div>
        </el-tab-pane>
    </el-tabs>
</div>
</template>

<script setup>
import { useMouse } from "@vueuse/core";
const { x, y } = useMouse();

import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const params = [{
    key: "@vueuse/core",
    value: "https://unpkg.com/@vueuse/core/index.mjs"
}, {
    key: "@vueuse/shared",
    value: "https://unpkg.com/@vueuse/shared/index.mjs"
}];
const js = `import { useMouse } from "@vueuse/core";
const { x, y } = useMouse();`;
const html = `<div class="grid grid-flow-col grid-gap-4 place-content-center place-items-center font-mono">
    <div class="font-mono bg-light-500 dark:bg-dark-500 flex flex-col text-center p-2 border-rounded">
        <span class="text-4xl">{{ x }}</span>
        <span class="text-sm dark:text-light-900 dark:text-opacity-50 mt-2">Mouse X</span>
    </div>
    <div class="font-mono bg-light-500 dark:bg-dark-500 flex flex-col text-center p-2 border-rounded">
        <span class="text-4xl">{{ y }}</span>
        <span class="text-sm dark:text-light-900 dark:text-opacity-50 mt-2">Mouse Y</span>
    </div>
</div>`;

</script>


