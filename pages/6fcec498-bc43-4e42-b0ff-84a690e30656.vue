<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <el-text>{{ t("site") }}: <a href="https://vuetifyjs.com" target="_blank">https://vuetifyjs.com</a></el-text>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Importmap</h3>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
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
                <v-card class="ma-4 max-w-96">
                    <v-img class="align-end text-white h-52" src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
                        cover>
                        <v-card-title>Top 10 Australian beaches</v-card-title>
                    </v-img>
                    <v-card-subtitle class="pt-4">Number 10</v-card-subtitle>
                    <v-card-text>
                        <div>Whitehaven Beach</div>
                        <div>Whitsunday Island, Whitsunday Islands</div>
                    </v-card-text>
                    <v-card-actions>
                        <v-btn color="orange" text="Share"></v-btn>
                        <v-btn color="orange" text="Explore"></v-btn>
                    </v-card-actions>
                </v-card>
            </el-tab-pane>
            <el-tab-pane label="Template">
                <highlightjs language="html" :code="html"></highlightjs>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script setup>
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
    { id } = defineProps(["id"]),
    the = inject("pages")[id],
    params = [{
        key: "vuetify",
        value: "https://cdn.jsdelivr.net/npm/vuetify/dist/vuetify.esm.js"
    }],
    js = `import "https://cdn.jsdelivr.net/npm/vuetify/dist/vuetify.min.css";
import { createVuetify, components, directives } from "vuetify";

window.app.use(createVuetify({ components, directives }));`,
    html = `<v-card class="ma-4 max-w-96">
    <v-img class="align-end text-white h-52" src="https://cdn.vuetifyjs.com/images/cards/docks.jpg" cover>
        <v-card-title>Top 10 Australian beaches</v-card-title>
    </v-img>
    <v-card-subtitle class="pt-4">Number 10</v-card-subtitle>
    <v-card-text>
        <div>Whitehaven Beach</div>
        <div>Whitsunday Island, Whitsunday Islands</div>
    </v-card-text>
    <v-card-actions>
        <v-btn color="orange" text="Share"></v-btn>
        <v-btn color="orange" text="Explore"></v-btn>
    </v-card-actions>
</v-card>`;
</script>

<style scoped src="./node_modules/vuetify/dist/vuetify.min.css"></style>
