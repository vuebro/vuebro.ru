<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
       <el-text>Сайт проекта: <a href="https://vueuse.org" target="_blank">https://vueuse.org</a></el-text>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Importmap</h3>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4">
            <template v-for="{ key, value } in params">
                <dt class="font-bold text-slate-700">{{ key }}</dt>
                <dd class="text-slate-500 overflow-hidden text-ellipsis">{{ value }}</dd>
            </template>
        </dl>
        <h3 class="mt-8 mb-3 !font-semibold !text-2xl">Пример использования</h3>
        <el-tabs class="not-prose 2xl:row-start-auto">
            <el-tab-pane label="Результат">
                <div class="flex justify-center items-center box-border perspective-300 h-48">
                    <div class="cube cursor-all-scroll relative w-100px h-100px preserve-3d [&>*]:absolute [&>*]:top-0 [&>*]:left-0 [&>*]:w-full [&>*]:h-full [&>*]:b-1 [&>*]:b-solid [&>*]:backface-hidden [&>*]:bg-emerald-4 [&>*]:bg-opacity-20 [&>*]:bg-center [&>*]:bg-[length:75%] [&>*]:bg-no-repeat"
                        @mousedown.capture="lock" @mouseup="unlock">
                        <span class="base bg-[url(https://vueuse.org/vue.svg)]" style="--i: 1"></span>
                        <span class="base bg-[url(https://vueuse.org/favicon.svg)]" style="--i: -1"></span>
                        <span class="side bg-[url(https://vueuse.org/vue.svg)]" style="--i: 0"></span>
                        <span class="side bg-[url(https://vueuse.org/favicon.svg)]" style="--i: 1"></span>
                        <span class="side bg-[url(https://vueuse.org/vue.svg)]" style="--i: 2"></span>
                        <span class="side bg-[url(https://vueuse.org/favicon.svg)]" style="--i: 3"></span>
                    </div>
                </div>
            </el-tab-pane>
            <el-tab-pane label="Template">
                <highlightjs language="html" :code="html"></highlightjs>
            </el-tab-pane>
            <el-tab-pane label="Script">
                <highlightjs language="js" :code="js"></highlightjs>
            </el-tab-pane>
            <el-tab-pane label="Style">
                <highlightjs language="css" :code="css"></highlightjs>
            </el-tab-pane>
        </el-tabs>
    </div>
</template>

<script setup>
import { useMouse, usePointerLock } from "@vueuse/core";
import { inject, shallowRef, watch } from "vue";

const { id } = defineProps(["id"]),
    the = inject("pages")[id], params = [{
        key: "@vueuse/core",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/core/index.mjs"
    }, {
        key: "@vueuse/shared",
        value: "https://cdn.jsdelivr.net/npm/@vueuse/shared/index.mjs"
    }],
    js = `import { useMouse, usePointerLock } from "@vueuse/core";
import { shallowRef, watch } from "vue";

const { lock, unlock, element } = usePointerLock(),
    type = "movement",
    { x, y } = useMouse({ type }),
    rotY = shallowRef(-45),
    rotX = shallowRef(0);

watch([x, y], ([x, y]) => {
    if (!element.value) return;
    rotY.value += x / 2;
    rotX.value -= y / 2;
})`;
const html = `<div class="flex justify-center items-center box-border perspective-300 h-48">
    <div class="cube cursor-all-scroll relative w-100px h-100px preserve-3d [&>*]:absolute [&>*]:top-0 [&>*]:left-0 [&>*]:w-full [&>*]:h-full [&>*]:b-1 [&>*]:b-solid [&>*]:backface-hidden [&>*]:bg-emerald-4 [&>*]:bg-opacity-20 [&>*]:bg-center [&>*]:bg-[length:75%] [&>*]:bg-no-repeat"
        @mousedown.capture="lock" @mouseup="unlock">
        <span class="base bg-[url(https://vueuse.org/vue.svg)]" style="--i: 1"></span>
        <span class="base bg-[url(https://vueuse.org/favicon.svg)]" style="--i: -1"></span>
        <span class="side bg-[url(https://vueuse.org/vue.svg)]" style="--i: 0"></span>
        <span class="side bg-[url(https://vueuse.org/favicon.svg)]" style="--i: 1"></span>
        <span class="side bg-[url(https://vueuse.org/vue.svg)]" style="--i: 2"></span>
        <span class="side bg-[url(https://vueuse.org/favicon.svg)]" style="--i: 3"></span>
    </div>
</div>`,
    css = `.cube {
    --rotY: v-bind(rotY);
    --rotX: v-bind(rotX);
    transform: rotateY(calc(var(--rotY) * 1deg)) rotateX(calc(var(--rotX) * 1deg));
}
.base {
    transform: rotateX(calc(90deg * var(--i))) translateZ(50px);
}
.side {
    transform: rotateY(calc(90deg * var(--i))) translateZ(50px);
}`;

const { lock, unlock, element } = usePointerLock(),
    type = "movement",
    { x, y } = useMouse({ type }),
    rotY = shallowRef(-45),
    rotX = shallowRef(0);

watch([x, y], ([x, y]) => {
    if (!element.value) return;
    rotY.value += x / 2;
    rotX.value -= y / 2;
})

</script>

<style scoped>
.cube {
    --rotY: v-bind(rotY);
    --rotX: v-bind(rotX);
    transform: rotateY(calc(var(--rotY) * 1deg)) rotateX(calc(var(--rotX) * 1deg));
}

.base {
    transform: rotateX(calc(90deg * var(--i))) translateZ(50px);
}

.side {
    transform: rotateY(calc(90deg * var(--i))) translateZ(50px);
}
</style>
