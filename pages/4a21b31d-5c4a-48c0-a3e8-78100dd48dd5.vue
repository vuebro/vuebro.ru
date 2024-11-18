<template>
<div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="pa-4 shadow-lg rounded-3xl border border-black/10 mb-14">
        <ul class="divide-y divide-slate-100 not-prose">
            <li v-for="{to, title, description, icon} in links">
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
    title: "Хостинг",
    description: "Создайте хостинг статических сайтов по инструкции.",
    to: "https://yandex.cloud/ru/docs/storage/operations/hosting/own-domain"
}, {
    icon: "ph:number-circle-two-duotone",
    title: "CORS",
    description: "Сконфигурируйте CORS. Установите \"Allowed Origins\" в \"*\", \"Allowed Methods\" в \"GET, PUT, HEAD\" и \"Allowed Headers\" в \"*, Authorization\".",
    to: "https://yandex.cloud/ru/docs/storage/operations/buckets/cors"
}, {
    icon: "ph:number-circle-three-duotone",
    title: "Аккаунт",
    description: "Создайте сервисный аккаунт.",
    to: "https://yandex.cloud/ru/docs/iam/operations/sa/create"
}, {
    icon: "ph:number-circle-four-duotone",
    title: "ACL",
    description: "Выдайте созданному в пердыдущем шаге сервисному аккаунту разрешения \"READ & WRITE\" для бакета, в котором хранятся файлы статического хостинга.",
    to: "https://yandex.cloud/ru/docs/storage/operations/buckets/edit-acl"
}, {
    icon: "ph:number-circle-five-duotone",
    title: "Ключи",
    description: "Создайте статические ключи доступа и сохраните их. Они пригодятся для входа через Vue.S3",
    to: "https://yandex.cloud/ru/docs/iam/operations/sa/create-access-key"
}];
const params = [{
    key: "bucket",
    value: "название бакета, совпадающее с доменом"
}, {
    key: "access key id",
    value: "id статического ключа доступа"
}, {
    key: "secret access key",
    value: "статический ключ доступа"
}, {
    key: "endpoint url",
    value: "https://storage.yandexcloud.net"
}, {
    key: "region",
    value: "ru-central1"
}];
</script>


