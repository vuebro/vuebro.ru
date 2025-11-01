<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <el-text>{{ t("site") }}: <a href="https://tresjs.org" target="_blank">https://tresjs.org</a></el-text>
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
                <div class="size-96">
                    <TresCanvas clear-color="white">
                        <Levioso :speed="2" :range="[0, 0.7]" :rotation-factor="9">
                            <TorusKnot :scale="0.45">
                                <TresMeshNormalMaterial />
                            </TorusKnot>
                        </Levioso>
                        <ContactShadows :position-y="-1" color="#335" :scale="20" />
                    </TresCanvas>
                </div>
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

<script setup vapor>
import { inject } from "vue";
import { useI18n } from "vue-i18n";
import { ContactShadows, Levioso, TorusKnot } from "https://cdn.jsdelivr.net/npm/@tresjs/cientos@5.1.0/dist/trescientos.js";
import { TresCanvas } from "@tresjs/core";

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
        key: "@tresjs/core",
        value: "https://cdn.jsdelivr.net/npm/@tresjs/core@5/dist/tres.js"
    }, {
        key: "@tresjs/cientos",
        value: "https://cdn.jsdelivr.net/npm/@tresjs/cientos@5/dist/trescientos.js"
    }, {
        key: "three",
        value: "https://cdn.jsdelivr.net/npm/three@0.180/build/three.module.min.js"
    }, {
        key: "@vueuse/core",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/core@14/dist/index.js"
    }, {
        key: "@vueuse/shared",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/shared@14/dist/index.js"
    }],
    html = `<TresCanvas clear-color="white">
    <Levioso :speed="2" :range="[0, 0.7]" :rotation-factor="9">
      <TorusKnot :scale="0.45">
        <TresMeshNormalMaterial />
      </TorusKnot>
    </Levioso>
    <ContactShadows :position-y="-1" color="#335" :scale="20" />
  </TresCanvas>`,
    script = `import { ContactShadows, Levioso, TorusKnot } from '@tresjs/cientos'
import { TresCanvas } from '@tresjs/core'`;


</script>
