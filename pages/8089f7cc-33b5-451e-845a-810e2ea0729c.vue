<template>
<div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="pa-4 shadow-lg rounded-3xl border border-black/10 mb-14">
        <ul class="divide-y divide-slate-100 not-prose">
            <li v-for="{to, title, description, icon, images} in links">
                <a :href="to" target="_blank" rel="noopener noreferrer"
                    class="flex items-start gap-4 px-4 py-3 hover:bg-slate-50">
                    <div class="flex items-center text-emerald-500">
                        <icon :icon="icon" class="size-6"></icon>
                    </div>
                    <div
                        class="flex flex-col gap-0 min-h-[2rem] items-start justify-center w-full min-w-0 overflow-hidden">
                        <h4 class="w-full text-base truncate text-slate-700">{{ title }}</h4>
                        <p class="w-full text-sm text-slate-500">{{ description }}</p>
                    </div>
                    <icon class="size-5 transition-colors text-slate-500 hover:text-emerald-500"
                        icon="ion:open-outline">
                    </icon>
                </a>
                <div class="ml-14 grid gap-8 grid-cols-1 md:grid-cols-2 w-96 items-center"><el-image fit="scale-down"
                        v-for="(src, index) in images" :src="src" :preview-src-list="images" :initial-index="index"
                        class="h-36 my-12 shadow-md rounded-lg border border-black/10"></el-image></div>
            </li>
        </ul>
    </div>
    <el-divider>⭐</el-divider>
    <h4 class="mt-12">После выполнения всех шагов эти параметры пригодятся для подключения vueS3 к хранилищу</h4>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
        <template v-for="{ key, value } in params">
            <dt class="font-bold text-slate-700"><el-tag class="w-full !justify-start" type="success">{{ key }}</el-tag>
            </dt>
            <dd class="text-slate-500">{{ value }}</dd>
        </template>
    </dl>
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];
const links = [{
    icon: "ph:number-circle-one-duotone",
    title: "Bucket",
    description: "Создайте бакет R2 по имени домена. Точку в имени домена замените на дефис (example.com => example-com).",
    to: "https://developers.cloudflare.com/r2/buckets/create-buckets/"
}, {
    icon: "ph:number-circle-two-duotone",
    title: "CORS",
    description: "Сконфигурируйте CORS. Файл конфигурации: [{\"AllowedOrigins\":[\"*\"],\"AllowedMethods\":[\"GET\",\"PUT\",\"HEAD\"],\"AllowedHeaders\":[\"*\",\"Authorization\"]}]",
    to: "https://developers.cloudflare.com/r2/buckets/cors/"
}, {
    icon: "ph:number-circle-three-duotone",
    title: "API Tokens",
    description: "Получите ключи доступа и эндпоинт",
    to: "https://developers.cloudflare.com/r2/api/s3/tokens/"
}, {
    icon: "ph:number-circle-four-duotone",
    title: "Custom domain",
    description: "Подключите домен",
    to: "https://developers.cloudflare.com/r2/buckets/public-buckets/#connect-a-bucket-to-a-custom-domain"
}, {
    icon: "ph:number-circle-five-duotone",
    title: "Rewrite index.html",
    description: "Создайте правило для переадресации с index.html: (ends_with(http.request.uri.path, \"/\")) => concat(http.request.uri.path, \"index.html\")",
    images: ["images/cbdba601-370a-4964-8611-94a5b4e5becb.webp",
        "images/72c7d0a4-73f8-4e17-980b-43082731eb8d.webp"],
    to: "https://developers.cloudflare.com/rules/transform/url-rewrite/create-dashboard/"
}, {
    icon: "ph:number-circle-six-duotone",
    title: "Trailing slash",
    description: "Создайте правило для добавления трейлинг слэша: (not http.request.uri.path contains \".\" and not ends_with(http.request.uri.path, \"/\")) => concat(http.request.uri.path, \"/\")",
    images: ["images/6a9a3c3b-443b-40cc-b1ba-d16e2a5f661c.webp",
        "images/235bd18a-3516-4f53-994e-2da9d0d6dfb5.webp"],
    to: "https://developers.cloudflare.com/rules/url-forwarding/single-redirects/create-dashboard/"
}];
const params = [{
    key: "bucket",
    value: "название бакета, совпадающее с доменом, с заменой точки на дефис"
}, {
    key: "access key id",
    value: "id статического ключа доступа"
}, {
    key: "secret access key",
    value: "статический ключ доступа"
}, {
    key: "endpoint url",
    value: "эндпоинт"
}, {
    key: "region",
    value: "auto"
}];
</script>


