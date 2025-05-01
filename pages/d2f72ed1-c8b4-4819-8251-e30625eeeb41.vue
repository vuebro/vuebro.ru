<template>
    <div class="container mx-auto px-4" un-cloak>
        <div class="flex flex-col text-center not-prose mb-24">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <h2>{{ t("h_1") }}</h2>
        <p>{{ t("desc") }}</p>
        <highlightjs class="not-prose" language="js" :code="t('inj')"></highlightjs>
        <h2>{{ t("h_2") }}</h2>
        <el-tabs class="2xl:row-start-auto">
            <el-tab-pane label="Template" class="not-prose">
                <highlightjs language="html" :code="html"></highlightjs>
            </el-tab-pane>
            <el-tab-pane :label="t('result')">
                <h3>{{ the.parent.title }}</h3>
                <ul>
                    <li v-for="{ title } in the.$siblings">{{ title }}</li>
                </ul>
            </el-tab-pane>
        </el-tabs>
        <h2>{{ t("h_6") }}</h2>
        <h3>{{ t("h_3") }}</h3>
        <el-divider border-style="dashed"></el-divider>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
            <template v-for="(,key) in messages.en.nav">
                <dt class="font-bold text-slate-700">{{ key }}:</dt>
                <dd class="text-slate-500">{{ t(`nav.${key}`) }}</dd>
            </template>
        </dl>
        <h3>{{ t("h_4") }}</h3>
        <el-link href="https://ogp.me" target="_blank">The Open Graph protocol</el-link>
        <el-divider direction="vertical" />
        <el-link :href="t('href')" target="_blank">The Sitemap</el-link>
        <el-divider border-style="dashed"></el-divider>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
            <template v-for="(,key) in messages.en.seo">
                <dt class="font-bold text-slate-700">{{ key }}:</dt>
                <dd class="text-slate-500">{{ t(`seo.${key}`) }}</dd>
            </template>
        </dl>
        <h3>{{ t("h_5") }}</h3>
        <el-divider border-style="dashed"></el-divider>
        <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
            <template v-for="(,key) in messages.en.settings">
                <dt class="font-bold text-slate-700">{{ key }}:</dt>
                <dd class="text-slate-500">{{ t(`settings.${key}`) }}</dd>
            </template>
        </dl>
        <div class="not-prose flex mt-48">
            <el-button-group class="mx-auto">
                <el-button type="primary" :icon="ArrowLeft" :to="the.$prev.to" v-if="the.$prev" tag="router-link">{{
                    the.$prev.header }}</el-button>
                <el-button type="primary" v-if="the.$next" :to="the.$next.to" tag="router-link">{{ the.$next.header
                }}<el-icon class="el-icon--right">
                        <ArrowRight></ArrowRight>
                    </el-icon></el-button>
            </el-button-group>
        </div>
    </div>
</template>

<script setup>
import { inject } from "vue";
import { useI18n } from "vue-i18n";
import { ArrowLeft, ArrowRight } from "@element-plus/icons-vue";

const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const messages = {
    en: {
        href: "https://www.sitemaps.org",
        desc: "Each page receives a prop `id` with a unique identification number. Additionally, it is possible to inject an associative array of all semantic objects of the pages and retrieve the identification number of the currently selected page from the router object.",
        result: "Result",
        h_1: "Connection",
        h_2: "Usage Example",
        h_3: "Navigation Attributes",
        h_4: "SEO Attributes",
        h_5: "Page Settings Attributes",
        h_6: "List of Attributes",
        inj: `/** Import computed and inject */
import {'{'} computed, inject {'}'} from "vue";
/** Import the composable for the selected route */
import {'{'} useRoute {'}'} from "vue-router";
/** Get the ID of the current page */
const {'{'} id {'}'} = defineProps(["id"]);
/** Get the object of the selected route */
const route = useRoute();
/** Inject the array of semantic objects for the site's pages */
const pages = inject("pages");
/**  Get the semantic object of the current page */
const the = pages[id];
/** Compute the semantic object of the selected page */
const that = computed(() => pages[route.name]);`,
        nav: {
            $children: "Child pages of the current page, considering the 'enabled' attribute",
            $index: "Index of the current page in the $siblings array",
            $next: "Next page relative to the current page in the $siblings array",
            $prev: "Previous page relative to the current page in the $siblings array",
            $siblings: "Array of sibling pages including the current page, considering the 'enabled' attribute",
            parent: "Parent page of the current page",
            next: "Next page relative to the current page in the siblings array",
            prev: "Previous page relative to the current page in the siblings array",
            index: "Index of the current page in the siblings array",
            children: "Child pages of the current page",
            siblings: "Array of sibling pages including the current page",
            path: "Relative path to the current page",
            branch: "Array of pages from the root to the current page",
            to: "URL of the page for use in router-link, considering the 'loc' attribute"
        },
        seo: {
            type: "Type of content for the current page (the)",
            header: "Title of the current page (the)",
            description: "Description of the current page (the)",
            keywords: "Keywords for the current page (the)",
            loc: "Permanent URL of the current page (the)",
            changefreq: "Update frequency (for sitemap)",
            priority: "Priority (for sitemap)",
            lastmod: "Last modified date (for sitemap)",
            icon: "Favicon URL",
            images: "Array of objects {'{'}url, alt{'}'}, where: url - image URL, alt - image description",
            title: "Value of the 'header' attribute if set; otherwise, the value of the 'name' attribute"
        },
        settings: {
            id: "Unique identifier for the current page (the)",
            flat: "Joint or separate display of child pages of the current page (the)",
            class: "Array of CSS classes for the current page (the)",
            enabled: "Toggle for the availability of the current page (the)",
            name: "Short name of the current page (the), used to form the 'path' attribute",
            i: "The 'icon' attribute with the 'i-' prefix"
        }

    },
    ru: {
        href: "https://www.sitemaps.org/ru",
        desc: "Каждая страница получает пропс id с персональным идентификационным номером. Так же есть возможность инжектировать ассоциативный массив всех семантических объектов страниц и получить идентификационный номер выбранной в данный момент страницы из объекта роутера.",
        result: "Результат",
        h_1: "Подключение",
        h_2: "Пример использования",
        h_3: "Навигационные атрибуты",
        h_4: "SEO атрибуты",
        h_5: "Атрибуты настройки страницы",
        h_6: "Список атрибутов",
        inj: `/** Импортируем вычислитель и инжектор */
import {'{'} computed, inject {'}'} from "vue";
/** Импортируем композабл выбранного роута */
import {'{'} useRoute {'}'} from "vue-router";
/** Получаем id данной страницы */
const {'{'} id {'}'} = defineProps(["id"]);
/** Получаем объект выбранного роута */
const route = useRoute();
/** Инжектируем массив семантических объектов страниц сайта */
const pages = inject("pages");
/** Получаем семантический объект данной станицы */
const the = pages[id];
/** Вычисляем семантический объект выбранной страницы */
const that = computed(() => pages[route.name]);`,
        nav: {
            $children: "Дочерние страницы the с учетом атрибута enabled",
            $index: "Индекс страницы the в массиве $siblings",
            $next: "Следующая страница от the в массиве $siblings",
            $prev: "Предыдущая страница от the в массиве $siblings",
            $siblings: "Массив одноуровневых страниц со страницей the с учетом атрибута enabled",
            parent: "Родительская страница the",
            next: "Следующая страница от the в массиве siblings",
            prev: "Предыдущая страница от the в массиве siblings",
            index: "Индекс страницы the в массиве siblings",
            children: "Дочерние страницы the",
            siblings: "Массив одноуровневых страниц со страницей the",
            path: "Относительный путь до страницы the",
            branch: "Массив страниц от корневой до страницы the",
            to: "Урл страницы для подстановки в router-link с учетом атрибута loc"
        },
        seo: {
            type: "Тип содержимого страницы the",
            header: "Заголовок страницы the",
            description: "Описание страницы the",
            keywords: "Ключевые слова для страницы the",
            loc: "Постоянная ссылка страницы the",
            changefreq: "Частота обновления",
            priority: "Приоритет",
            lastmod: "Дата последнего изменения",
            icon: "Фавиконка",
            images: "Массив объектов {'{'}url, alt{'}'}, где: url - адрес картинки, alt - описание картинки",
            title: "Значение атрибута header, если задан, иначе значение атрибута name"
        },
        settings: {
            id: "Уникальный идентификатор страницы the",
            flat: "Совместное или раздельное представление дочерних страниц the",
            class: "Массив классов страницы the",
            enabled: "Переключатель доступности страницы the",
            name: "Короткое имя страницы the, используется для формирования атрибута path",
            i: "Атрибут icon с префиксом i-"
        }
    }
},
    { t } = useI18n({ messages });

const html = `<h3>{{ the.parent.title }}</h3>
<ul>
    <li v-for=\"{title} in the.$siblings\">{{ title }}</li>
</ul>`;
</script>
