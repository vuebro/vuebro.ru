<template>
    <div class="container mx-auto px-4" un-cloak>
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <div class="pa-4 shadow-lg rounded-3xl border border-black/10 my-28">
            <ul class="divide-y divide-slate-100 not-prose">
                <li v-for="{ to, title, description, icon } in links">
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
        <h4 class="mt-28">{{ t("does") }}</h4>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit mt-12">
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

const { t, locale } = useI18n({
    messages: {
        en: {
            hosingTitle: "Hosting",
            hosting: "Create a static website hosting according to the instructions.",
            cors: 'Configure CORS. Set "Allowed Origins" to "*", "Allowed Methods" to "*", and "Allowed Headers" to "*, Authorization".',
            accountTitle: "Account",
            account: "Create a service account.",
            acl: 'Grant the service account created in the previous step "READ & WRITE" permissions for the bucket where the static hosting files are stored.',
            keysTitle: "Keys",
            keys: "Create static access keys and save them. They will be useful for logging in to VueBro.",
            does: "After completing all the steps, these parameters will be useful for connecting VueBro to the storage.",
            bucket: "bucket name, matching the domain",
            accesskey: "static access key ID",
            secretaccesskey: "static access key"
        },
        ru: {
            hosingTitle: "Хостинг",
            hosting: "Создайте хостинг статических сайтов по инструкции.",
            cors: 'Сконфигурируйте CORS. Установите "Allowed Origins" в "*", "Allowed Methods" в "*" и "Allowed Headers" в "*, Authorization".',
            accountTitle: "Аккаунт",
            account: "Создайте сервисный аккаунт.",
            acl: 'Выдайте созданному в пердыдущем шаге сервисному аккаунту разрешения "READ & WRITE" для бакета, в котором хранятся файлы статического хостинга.',
            keysTitle: "Ключи",
            keys: "Создайте статические ключи доступа и сохраните их. Они пригодятся для входа через VueBro",
            does: "После выполнения всех шагов эти параметры пригодятся для подключения VueBro к хранилищу",
            bucket: "название бакета, совпадающее с доменом",
            accesskey: "id статического ключа доступа",
            secretaccesskey: "статический ключ доступа"
        }
    }
}),
    { id } = defineProps(["id"]),
    the = inject("pages")[id],
    links = reactive([{
        icon: "ph:number-circle-one-duotone",
        title: t("hosingTitle"),
        description: t("hosting"),
        to: `https://yandex.cloud/${locale.value}/docs/storage/operations/hosting/own-domain`
    }, {
        icon: "ph:number-circle-two-duotone",
        title: "CORS",
        description: t("cors"),
        to: `https://yandex.cloud/${locale.value}/docs/storage/operations/buckets/cors`
    }, {
        icon: "ph:number-circle-three-duotone",
        title: t("accountTitle"),
        description: t("account"),
        to: `https://yandex.cloud/${locale.value}/docs/iam/operations/sa/create`
    }, {
        icon: "ph:number-circle-four-duotone",
        title: "ACL",
        description: t("acl"),
        to: `https://yandex.cloud/${locale.value}/docs/storage/operations/buckets/edit-acl`
    }, {
        icon: "ph:number-circle-five-duotone",
        title: t("keysTitle"),
        description: t("keys"),
        to: `https://yandex.cloud/${locale.value}/docs/iam/operations/sa/create-access-key`
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
        value: "https://storage.yandexcloud.net"
    }, {
        key: "region",
        value: "ru-central1"
    }]);
</script>
