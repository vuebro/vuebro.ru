<template>
    <div class="container mx-auto px-4" un-cloak>
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <div class="pa-4 shadow-lg rounded-3xl border border-black/10 my-28">
            <ul class="divide-y divide-slate-100 not-prose">
                <li v-for="{ to, title, description, icon, images } in links">
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
                    <div class="ml-13 mt-4 mb-8 grid gap-8 grid-cols-1 md:grid-cols-2 max-w-192 items-center" v-if="images?.length"><el-image
                            fit="scale-down" v-for="(src, index) in images" :src="src" :preview-src-list="images"
                            :initial-index="index"
                            class="h-36 shadow-md rounded-lg border border-black/10 max-w-96"></el-image></div>
                </li>
            </ul>
        </div>
        <el-divider>⭐</el-divider>
        <h4 class="mt-28">{{ t("does") }}</h4>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit mt-12 not-prose">
            <template v-for="{ key, value } in params">
                <dt class="font-bold text-slate-700"><el-tag class="w-full !justify-start" type="success">{{ key
                }}</el-tag>
                </dt>
                <dd class="text-slate-500 text-ellipsis overflow-hidden">{{ value }}</dd>
            </template>
        </dl>
    </div>
</template>

<script setup vapor>
import { inject, reactive } from "vue";
import { useI18n } from "vue-i18n";

const { t } = useI18n({
    messages: {
        en: {
            hosingTitle: "Bucket",
            hosting: "Create an R2 bucket named after the domain. Replace the dot in the domain name with a hyphen (example.com => example-com).",
            cors: "Configure CORS. Configuration file: [{'{\"AllowedOrigins\":[\"*\"],\"AllowedMethods\":[\"*\"],\"AllowedHeaders\":[\"*\",\"Authorization\"]}'}]",
            tokens: "Obtain the access keys and an endpoint url",
            domain: "Connect a domain",
            rewriteindex: "Create a rule for redirecting to index.html: (ends_with(http.request.uri.path, \"/\")) => concat(http.request.uri.path, \"index.html\")",
            trailingslash: "Create a rule for adding a trailing slash: (not http.request.uri.path contains \".\" and not ends_with(http.request.uri.path, \"/\")) => concat(http.request.uri.path, \"/\")",
            does: "After completing all the steps, these parameters will be useful for connecting VueBro to the storage.",
            bucket: "bucket name matching the domain, with dots replaced by hyphens",
            accesskey: "static access key ID",
            secretaccesskey: "static access key",
            endpoint: "the endpoint"
        },
        ru: {
            hosingTitle: "Бакет",
            hosting: "Создайте бакет R2 по имени домена. Точку в имени домена замените на дефис (example.com => example-com).",
            cors: "Сконфигурируйте CORS. Файл конфигурации: [{'{\"AllowedOrigins\":[\"*\"],\"AllowedMethods\":[\"*\"],\"AllowedHeaders\":[\"*\",\"Authorization\"]}'}]",
            tokens: "Получите ключи доступа и эндпоинт",
            domain: "Подключите домен",
            rewriteindex: "Создайте правило для переадресации с index.html: (ends_with(http.request.uri.path, \"/\")) => concat(http.request.uri.path, \"index.html\")",
            trailingslash: "Создайте правило для добавления трейлинг слэша: (not http.request.uri.path contains \".\" and not ends_with(http.request.uri.path, \"/\")) => concat(http.request.uri.path, \"/\")",
            does: "После выполнения всех шагов эти параметры пригодятся для подключения VueBro к хранилищу",
            bucket: "название бакета, совпадающее с доменом, с заменой точки на дефис",
            accesskey: "id статического ключа доступа",
            secretaccesskey: "статический ключ доступа",
            endpoint: "эндпоинт"
        }
    }
}),
    { id } = defineProps(["id"]),
    the = inject("pages")[id],
    links = reactive([{
        icon: "ph:number-circle-one-duotone",
        title: t("hosingTitle"),
        description: t("hosting"),
        to: "https://developers.cloudflare.com/r2/buckets/create-buckets/"
    }, {
        icon: "ph:number-circle-two-duotone",
        title: "CORS",
        description: t("cors"),
        to: "https://developers.cloudflare.com/r2/buckets/cors/"
    }, {
        icon: "ph:number-circle-three-duotone",
        title: "API Tokens",
        description: t("tokens"),
        to: "https://developers.cloudflare.com/r2/api/s3/tokens/"
    }, {
        icon: "ph:number-circle-four-duotone",
        title: "Custom domain",
        description: t("domain"),
        to: "https://developers.cloudflare.com/r2/buckets/public-buckets/#connect-a-bucket-to-a-custom-domain"
    }, {
        icon: "ph:number-circle-five-duotone",
        title: "Rewrite index.html",
        description: t("rewriteindex"),
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
    }]),
    params = reactive([{
        key: "bucket",
        value: t("bucket")
    }, {
        key: "access key id",
        value: t("accesskey")
    }, {
        key: "secret access key",
        value: t("secretaccesskey")
    }, {
        key: "endpoint url",
        value: t("endpoint")
    }, {
        key: "region",
        value: "auto"
    }]);
</script>
