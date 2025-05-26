<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <el-text>{{ t("site") }}: <a href="https://tresjs.org" target="_blank">https://tresjs.org</a></el-text>
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
                <div class="size-96">
                    <TresCanvas v-bind="gl">
                        <TresPerspectiveCamera :args="[450, 1, 0.1, 1000]"></TresPerspectiveCamera>
                        <TresMesh :position="[-2, 2, 0]" :rotation="[0, Math.PI, 0]">
                            <TresConeGeometry :args="[1, 1.5, 3]"></TresConeGeometry>
                            <TresMeshToonMaterial color="#82DBC5"></TresMeshToonMaterial>
                        </TresMesh>
                        <TresMesh ref="boxRef" cast-shadow :position="[0, 0, 0]">
                            <TresBoxGeometry :args="[1.5, 1.5, 1.5]"></TresBoxGeometry>
                            <TresMeshToonMaterial color="#4F4F4F"></TresMeshToonMaterial>
                        </TresMesh>
                        <TresMesh cast-shadow :position="[2, -2, 0]">
                            <TresSphereGeometry></TresSphereGeometry>
                            <TresMeshToonMaterial color="#FBB03B"></TresMeshToonMaterial>
                        </TresMesh>
                        <TresMesh receive-shadow :position="[0, -3, 0]" :rotation="[-Math.PI / 2, 0, 0]">
                            <TresPlaneGeometry :args="[10, 10, 10, 10]"></TresPlaneGeometry>
                            <TresMeshStandardMaterial color="#f7f7f7"></TresMeshStandardMaterial>
                        </TresMesh>
                        <TresAmbientLight :intensity="1"></TresAmbientLight>
                        <TresDirectionalLight cast-shadow :position="[0, 2, 0]" :intensity="1"></TresDirectionalLight>
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
import { inject, getCurrentInstance, shallowRef } from "vue";
import { useI18n } from "vue-i18n";
import Tres, { TresCanvas, useRenderLoop } from "https://cdn.jsdelivr.net/npm/@tresjs/core@4/dist/tres.js";
import { BasicShadowMap, SRGBColorSpace, NoToneMapping } from "three";

const { appContext: { app } } = getCurrentInstance(),
    { t } = useI18n({
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
        value: "https://cdn.jsdelivr.net/npm/@tresjs/core@4/dist/tres.js"
    }, {
        key: "three",
        value: "https://cdn.jsdelivr.net/npm/three/build/three.module.min.js"
    }, {
        key: "@vueuse/core",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/core@13/index.mjs"
    }, {
        key: "@vueuse/shared",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/shared@13/index.mjs"
    }],
    js = `<script setup>
import { getCurrentInstance } from "vue";
import Tres from "@tresjs/core";
const { appContext: { app } } = getCurrentInstance();
app.use(Tres);
<\/script>`,
    html = `<TresCanvas v-bind="gl">
    <TresPerspectiveCamera :args="[450, 1, 0.1, 1000]"></TresPerspectiveCamera>
    <TresMesh :position="[-2, 2, 0]" :rotation="[0, Math.PI, 0]">
        <TresConeGeometry :args="[1, 1.5, 3]"></TresConeGeometry>
        <TresMeshToonMaterial color="#82DBC5"></TresMeshToonMaterial>
    </TresMesh>
    <TresMesh ref="boxRef" cast-shadow :position="[0, 0, 0]">
        <TresBoxGeometry :args="[1.5, 1.5, 1.5]"></TresBoxGeometry>
        <TresMeshToonMaterial color="#4F4F4F"></TresMeshToonMaterial>
    </TresMesh>
    <TresMesh cast-shadow :position="[2, -2, 0]">
        <TresSphereGeometry></TresSphereGeometry>
        <TresMeshToonMaterial color="#FBB03B"></TresMeshToonMaterial>
    </TresMesh>
    <TresMesh receive-shadow :position="[0, -3, 0]" :rotation="[-Math.PI / 2, 0, 0]">
        <TresPlaneGeometry :args="[10, 10, 10, 10]"></TresPlaneGeometry>
        <TresMeshStandardMaterial color="#f7f7f7"></TresMeshStandardMaterial>
    </TresMesh>
    <TresAmbientLight :intensity="1"></TresAmbientLight>
    <TresDirectionalLight cast-shadow :position="[0, 2, 0]" :intensity="1"></TresDirectionalLight>
</TresCanvas>`,
    script = `import { shallowRef } from "vue";
import { TresCanvas, useRenderLoop } from "@tresjs/core";
import { BasicShadowMap, SRGBColorSpace, NoToneMapping } from "three";

const gl = {
  clearColor: "#82DBC5",
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping,
};
const boxRef = shallowRef();
const { onLoop } = useRenderLoop();

onLoop(() => {
  if(boxRef.value) boxRef.value.rotation.y += 0.01;
});`,
    gl = {
        clearColor: '#82DBC5',
        shadows: true,
        alpha: false,
        shadowMapType: BasicShadowMap,
        outputColorSpace: SRGBColorSpace,
        toneMapping: NoToneMapping,
    },
    boxRef = shallowRef(),
    { onLoop } = useRenderLoop();

app.use(Tres);

onLoop(() => {
    if (boxRef.value) boxRef.value.rotation.y += 0.01;
});

</script>

<style scoped src="https://cdn.jsdelivr.net/npm/quasar@2/dist/quasar.prod.css"></style>