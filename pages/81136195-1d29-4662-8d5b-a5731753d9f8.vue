<template>
    <div class="justify-center flex flex-wrap gap-2 mb-12" un-cloak>
        <span v-if="title">
            <el-button size="large" type="primary" round :to="to" tag="router-link" class="w-48">
                <icon :icon="startIcon" class="size-6 mr-1"></icon>
                {{ title }}
                <el-icon class="el-icon--right">
                    <ArrowRight />
                </el-icon>
            </el-button>
        </span>
        <span v-for="{ brandIcon, text, link } in social">
            <el-button tag="a" :href="link" target="_blank" size="large" type="plain" round class="w-48">
                <icon :icon="brandIcon" class="size-6 mr-1"></icon>
                {{ text }}
                <el-icon class="el-icon--right">
                    <ArrowRight />
                </el-icon>
            </el-button>
        </span>
    </div>
</template>

<script setup lang="js">
import { ArrowRight } from "@element-plus/icons-vue";

import { inject } from "vue";

const { $children: [{ title, to, icon: startIcon } = {}] = [] } = Object.values(inject("pages")).find(({ name }) => name === "документация") ?? {};

const social = [
    { brandIcon: "fa6-brands:github", text: "vueS3 на github", link: "https://github.com/vues3" },
    { brandIcon: "fa6-brands:vk", text: "vueS3 вконтакте", link: "https://vk.com/vues3" }
];
</script>