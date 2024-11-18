<template>
<div class="container mx-auto px-4">
  <div class="flex flex-col text-center not-prose">
    <icon :icon="the.icon" class="size-20 mx-auto"></icon>
    <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
    <el-text size="large">{{ the.description }}</el-text>
  </div>
    <h3>Подключение</h3>
    <p>Каждая страница получает пропс id с персональным идентификационным номером.
        Так же есть возможность инжектировать ассоциативный массив всех семантических объектов страниц и
        идентификационный номер выбранной в данный момент страницы.</p>
    <highlightjs class="not-prose" language="js" :code="inj"></highlightjs>
    <h3>Пример использования</h3>
    <el-tabs class="2xl:row-start-auto">
        <el-tab-pane label="Template" class="not-prose">
            <highlightjs language="html" :code="html"></highlightjs>
        </el-tab-pane>
        <el-tab-pane label="Результат">
            <h3>{{ the.parent.title }}</h3>
            <ul>
                <li v-for="{title} in the.$siblings">{{ title }}</li>
            </ul>
        </el-tab-pane>
    </el-tabs>
    <h3>Навигационные атрибуты</h3>
    <el-divider border-style="dashed"></el-divider>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
        <template v-for="{ key, description } in nav">
            <dt class="font-bold text-slate-700">{{ key }}:</dt>
            <dd class="text-slate-500">{{ description }}</dd>
        </template>
    </dl>
    <h3>SEO атрибуты</h3>
    <el-link href="https://ogp.me" target="_blank">The Open Graph protocol</el-link>
    <el-divider direction="vertical" />
    <el-link href="https://www.sitemaps.org/ru/" target="_blank">The Sitemap</el-link>
    <el-divider border-style="dashed"></el-divider>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
        <template v-for="{ key, description } in seo">
            <dt class="font-bold text-slate-700">{{ key }}:</dt>
            <dd class="text-slate-500">{{ description }}</dd>
        </template>
    </dl>
    <h3>Атрибуты настройки страницы</h3>
    <el-divider border-style="dashed"></el-divider>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
        <template v-for="{ key, description } in settings">
            <dt class="font-bold text-slate-700">{{ key }}:</dt>
            <dd class="text-slate-500">{{ description }}</dd>
        </template>
    </dl>
    <!--div class="not-prose flex my-12">
        <el-button-group class="mx-auto">
            <el-button type="primary" :icon="ArrowLeft" :to="the.$prev.to" v-if="the.$prev" tag="router-link">{{
                the.$prev.header }}</el-button>
            <el-button type="primary" v-if="the.$next" :to="the.$next.to" tag="router-link">{{ the.$next.header
                }}<el-icon class="el-icon--right">
                    <ArrowRight></ArrowRight>
                </el-icon></el-button>
        </el-button-group>
    </div-->
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const inj = `/** Импортируется вычислитель и инжектор */
import { computed, inject } from "vue";
/** Подключение id страницы из props */
const { id } = defineProps(["id"]);
/** Инжектирование ассоциативного массива семантических объектов страниц */
const pages = inject("pages");
/** Получение семантического объекта текущей страницы */
const the = pages[id];
/** Инжектирование id выбранной страницы */
const selId = inject("id");
/** Вычисление семантического объекта выбранной страницы */
const sel = computed(() => pages[selId.value]);`;

const html = `<h3>{{ the.parent.title }}</h3>
<ul>
    <li v-for=\"{title} in the.$siblings\">{{ title }}</li>
</ul>`;

const nav = [{
    key: "root", description: "Корневая страница"
}, {
    key: "$children", description: "Дочерние страницы the с учетом атрибута enabled"
}, {
    key: "$index", description: "Индекс страницы the в массиве $siblings"
}, {
    key: "$next", description: "Следующая страница от the в массиве $siblings"
}, {
    key: "$prev", description: "Предыдущая страница от the в массиве $siblings"
}, {
    key: "$siblings", description: "Массив одноуровневых страниц со страницей the с учетом атрибута enabled"
}, {
    key: "parent", description: "Родительская страница the"
}, {
    key: "next", description: "Следующая страница от the в массиве siblings"
}, {
    key: "prev", description: "Предыдущая страница от the в массиве siblings"
}, {
    key: "index", description: "Индекс страницы the в массиве siblings"
}, {
    key: "children", description: "Дочерние страницы the"
}, {
    key: "siblings", description: "Массив одноуровневых страниц со страницей the"
}, {
    key: "pages", description: "Массив всех страниц"
}, {
    key: "current", description: "Выбранная страница роутера"
}, {
    key: "path", description: "относительный путь до страницы the"
}, {
    key: "branch", description: "Массив страниц от корневой до страницы the"
}, {
    key: "to", description: "Урл страницы для подстановки в router-link с учетом атрибута loc"
},];

const seo = [{
    key: "type", description: "Тип содержимого страницы the"
}, {
    key: "header", description: "Заголовок страницы the"
}, {
    key: "description", description: "Описание страницы the"
}, {
    key: "keywords", description: "Ключевые слова для страницы the"
}, {
    key: "loc", description: "Постоянная ссылка страницы the"
}, {
    key: "changefreq", description: "Частота обновления"
}, {
    key: "priority", description: "Приоритет"
}, {
    key: "lastmod", description: "Дата последнего изменения"
}, {
    key: "icon", description: "Фавиконка"
}, {
    key: "image", description: "Массив объектов {url, alt}, где: url - адрес картинки, alt - описание картинки"
},
{
    key: "title", description: "Значение атрибута header, если задан, иначе значение атрибута name"
},];

const settings = [{ key: "id", description: "Уникальный идентификатор страницы the" },
{ key: "sfc", description: "Объект содержимого страницы the с атрибутами: template, script, style" }, {
    key: "along", description: "Совместное или раздельное представление дочерних страниц the"
}, {
    key: "class", description: "Массив классов страницы the"
}, {
    key: "enabled", description: "Переключатель доступности страницы the"
}, {
    key: "name", description: "Короткое имя страницы the, используется для формирования атрибута path"
},
{
    key: "scoped", description: "Установка атрибута scoped для атрибута style"
}, {
    key: "setup", description: "Установка атрибута setup для атрибута script"
}, {
    key: "i", description: "Атрибут icon с префиксом i-"
},];

</script>


