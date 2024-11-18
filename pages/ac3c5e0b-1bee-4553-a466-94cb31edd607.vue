<template>
<div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-12">
        <icon :icon="the.icon" class="size-20 mx-auto"></icon>
        <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
    <div class="not-prose gap-6 mb-12 flex flex-wrap justify-around">
        <template v-for="{icon, to, enabled, header} in the.children">
            <router-link :to="to" v-if="enabled" class="items-center text-center flex flex-col">
                <icon :icon="icon" class="size-24 ma-6 hover:text-slate-600 transition-colors"></icon>
                <el-text tag="b">{{ header }}</el-text>
            </router-link>
            <div v-else class="items-center text-center flex flex-col">
                <icon :icon="icon" class="size-24 ma-6 text-slate-400"></icon>
                <el-text tag="b">{{ header }}</el-text>
            </div>
        </template>
    </div>
    <el-alert title="Зачем создавать облачный хостинг?" :closable="false" show-icon class="shadow-md">
        Провайдеры облачных услуг, предоставляющие хранилище S3, позволяют использовать его в качестве хостинга
        статических сайтов.
        Создание хостинга осуществляется по инструкциям, опубликованным провайдером облачных услуг.
        Вы можете найти все необходимые инструкции, нажав на иконку с логотипом вашего провайдера.
        Как только хостинг будет создан, войдите на него с помощью Vue.S3 и приступайте к созданию сайта.
    </el-alert>
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

</script>


