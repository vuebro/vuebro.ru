<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <el-text>Сайт проекта: <a href="https://quasar.dev" target="_blank">https://quasar.dev</a></el-text>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Importmap</h3>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4">
            <template v-for="{ key, value } in params">
                <dt class="font-bold text-slate-700">{{ key }}</dt>
                <dd class="text-slate-500 overflow-hidden text-ellipsis">{{ value }}</dd>
            </template>
        </dl>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Код для подключения библиотеки</h3>
        <highlightjs language="js" :code="js" class="not-prose"></highlightjs>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Пример использования</h3>
        <el-tabs class="not-prose 2xl:row-start-auto">
            <el-tab-pane label="Результат">
                <q-card class="ma-4 max-w-96" flat bordered>
                    <q-img src="https://cdn.quasar.dev/img/parallax2.jpg" />
                    <q-card-section>
                        <div class="text-overline text-orange-9">Overline</div>
                        <div class="text-h5 q-mt-sm q-mb-xs">Title</div>
                        <div class="text-caption text-grey">
                            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut
                            labore
                            et dolore magna aliqua.
                        </div>
                    </q-card-section>
                    <q-card-actions>
                        <q-btn flat color="primary" label="Share" />
                        <q-btn flat color="secondary" label="Book" />
                    </q-card-actions>
                </q-card>
            </el-tab-pane>
            <el-tab-pane label="Template">
                <highlightjs language="html" :code="html"></highlightjs>
            </el-tab-pane>
            <el-tab-pane label="Script">
                <highlightjs language="js" :code="script"></highlightjs>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script setup>
import { inject } from "vue";
import { QCard, QImg, QCardSection, QCardActions, QBtn } from "quasar";

const { id } = defineProps(["id"]);
const the = inject("pages")[id];

const params = [{
    key: "quasar",
    value: "https://cdn.jsdelivr.net/npm/quasar/dist/quasar.client.js"
}];
const js = `import "https://cdn.jsdelivr.net/npm/quasar/dist/quasar.prod.css";
import { Quasar } from "quasar";

window.app.use(Quasar);`;
const html = `<q-card class="ma-4 max-w-96" flat bordered>
    <q-img src="https://cdn.quasar.dev/img/parallax2.jpg" />
    <q-card-section>
        <div class="text-overline text-orange-9">Overline</div>
        <div class="text-h5 q-mt-sm q-mb-xs">Title</div>
        <div class="text-caption text-grey">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
        </div>
    </q-card-section>
    <q-card-actions>
        <q-btn flat color="primary" label="Share" />
        <q-btn flat color="secondary" label="Book" />
    </q-card-actions>
</q-card>`,
    script = `import { QCard, QImg, QCardSection, QCardActions, QBtn } from "quasar";`;
</script>

<style scoped src="./node_modules/quasar/dist/quasar.prod.css"></style>

<style>
.absolute-full {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
}
</style>
