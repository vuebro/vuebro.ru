<template>
    <div class="container mx-auto px-4" un-cloak>
        <div class="flex flex-col text-center not-prose mb-24">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <h4>{{ t("h4") }}</h4>
        <ul class="not-prose list-none list-inside">
            <li v-for="leaf in tree"><el-text tag="b"><el-icon>
                        <Folder v-if="leaf.icon === 'folder'"></Folder>
                        <Document v-else></Document>
                    </el-icon> {{ leaf.name }}</el-text><el-text> - {{ leaf.description }}</el-text>
                <ul class="list-none list-inside ml-8" v-if="leaf.children">
                    <li>
                        <el-text tag="b">
                            <el-icon>
                                <Document></Document>
                            </el-icon> {{ leaf.children[0].name }}</el-text><el-text> - {{ leaf.children[0].description
                            }}</el-text>
                    </li>
                </ul>
            </li>
        </ul>
        <h3>{{ t("h3") }}</h3>
        <p>{{ t("p") }}</p>
        <div class="not-prose flex mt-48">
            <el-button-group class="mx-auto" size="large">
                <el-button class="my-1" type="primary" :icon="ArrowLeft" :to="the.$prev.to" v-if="the.$prev" tag="router-link">{{
                    the.$prev.header }}</el-button>
                <el-button  class="my-1" type="primary" v-if="the.$next" :to="the.$next.to" tag="router-link">{{ the.$next.header
                }}<el-icon class="el-icon--right">
                        <ArrowRight></ArrowRight>
                    </el-icon></el-button>
            </el-button-group>
        </div>
    </div>
</template>

<script setup vapor>
import { Folder, Document } from "@element-plus/icons-vue";
import { useI18n } from "vue-i18n";
import { inject, reactive } from "vue";
import { ArrowLeft, ArrowRight } from "@element-plus/icons-vue";

const { t } = useI18n({
    messages: {
        en: {
            h4: "This is the set of folders and files you will see after launching vueS3",
            h3: "Dynamic Folder Structure",
            p: "As you create categories in the tree structure of vueS3, folders corresponding to routes are created. An index.html file identical to the one in the root is placed into these folders, but with attributes corresponding to the route. The process of creating folders and updating index.html files is fully automatic and is intended to ensure SEO.",
            dsc1: "Folder for storing the Vite manifest",
            dsc1_1: "Manifest file used for synchronizing system modules",
            dsc2: "System modules that ensure the website’s functionality",
            dsc3: "Uploaded images",
            dsc4: "SFC components for each page",
            dsc5: "Boot file",
            dsc6: "Hierarchical structure of semantic attributes for all site pages",
            dsc7: "List of imported modules",
            dsc8: "Recommendations for search engines",
            dsc9: "Sitemap for search engines",
            dsc10: "Favicon",
            dsc11: "List of loaded fonts",
            dsc12: "Domain"
        },
        ru: {
            h4: "Такой набор папок и файлов вы увидите после запуска vueS3",
            h3: "Динамическая структура папок",
            p: "По мере создания рубрик в древовидной структуре vueS3, создаются папки соответствующие роутам. В созданные папки помещается файл index.html, идентичный тому, что находится в корне но с аттрибутами, соответствующими роуту. Процесс создания папок и обновления файлов index.html полностью автоматический и предназначен для обеспечения SEO.",
            dsc1: "папка для хранения манифеста vite",
            dsc1_1: "файл манифеста, предназначенный для синхронизации системных модулей",
            dsc2: "системные модули, обеспечивающие работоспособность сайта",
            dsc3: "загруженные изображения",
            dsc4: "sfc компоненты для каждой страницы",
            dsc5: "загрузочный файл",
            dsc6: "иерархическая структура семантических атрибутов всех страниц сайта",
            dsc7: "список импортируемых модулей",
            dsc8: "рекомендации для поисковиков",
            dsc9: "карта сайта для поисковиков",
            dsc10: "фавиконка",
            dsc11: "список подгружаемых шрифтов",
            dsc12: "домен",
        }
    }
});
const { id } = defineProps(["id"]),
    pages = inject("pages"),
    the = pages[id],
    tree = reactive([
        {
            icon: "folder", name: ".vite", description: t("dsc1"), children: [
                { name: "manifest.json", description: t("dsc1_1") },
            ]
        },
        { icon: "folder", name: "assets", description: t("dsc2") },
        { icon: "folder", name: "images", description: t("dsc3") },
        { icon: "folder", name: "pages", description: t("dsc4") },
        { icon: "document", name: "index.html", description: t("dsc5") },
        { icon: "document", name: "index.json ", description: t("dsc6") },
        { icon: "document", name: "index.importmap", description: t("dsc7") },
        { icon: "document", name: "robots.txt", description: t("dsc8") },
        { icon: "document", name: "sitemap.xml", description: t("dsc9") },
        { icon: "document", name: "favicon.ico", description: t("dsc10") },
        { icon: "document", name: "fonts.json", description: t("dsc11") },
        { icon: "document", name: "CNAME", description: t("dsc12") },
    ]);
</script>
