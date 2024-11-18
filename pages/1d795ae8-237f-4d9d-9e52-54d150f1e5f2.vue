<template>
<div class="container mx-auto px-4">
  <div class="flex flex-col text-center not-prose">
    <icon :icon="the.icon" class="size-20 mx-auto"></icon>
    <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
    <el-text size="large">{{ the.description }}</el-text>
  </div>
    <h3>Импортирование модулей</h3>
    <p>Инструкция import используется для импорта ссылок на значения, экспортированные из внешнего модуля.</p>
    <highlightjs :code="ex1" language="js" class="not-prose my-6"></highlightjs>
    <dl class="mb-6">
        <template v-for="{dt, dd} in ex1dl">
            <dt class="font-bold text-slate-700">{{ dt }}</dt>
            <dd class="text-slate-500">{{ dd }}</dd>
        </template>
    </dl>
    <h3>Сетевые источники пакетов</h3>
    <p>Онлайн доступ ко всем пакетам, предоставляемым через пакетный менеджер <a href="https://npmjs.com"
            target="_blank" rel="noopener noreferrer">npm</a> можно получить через веб сервисы, такие как:</p>
    <ul>
        <li><a href="https://unpkg.com" target="_blank" rel="noopener noreferrer">unpkg.com</a></li>
        <li><a href="https://jsdelivr.com" target="_blank" rel="noopener noreferrer">jsdelivr.com</a></li>
    </ul>
    <p>В современных пакетах обычно уже присутствует файл esm модуля для подключения. Если по какой-либо причине в
        пакете нет esm модуля, то можно
        воспользоваться сервисами, которые соберут для вас модуль из исходников пакета:</p>
    <ul>
        <li><a href="https://esm.sh" target="_blank" rel="noopener noreferrer">esm.sh</a></li>
        <li><a href="https://esm.run" target="_blank" rel="noopener noreferrer">esm.run</a></li>
    </ul>
    <p>Примеры подключения модулей популярных библиотек и фреймворков к vueS3: <router-link
            to="/модули/">модули</router-link></p>
    <h3>Использование importmap</h3>
    <div class="grid grid-cols-1 gap-6 lg:grid-cols-8">
        <div class="col-span-1 lg:col-span-5 text-justify">
            Для добавления
            модуля в importmap воспользуйтесь инструментом из выпадающего меню в правом верхнем углу
            основного окна vueS3. Importmap дает возможность использовать имена при импортировании модулей, что
            полезно, если имена
            используются при импортировании в модулях из онлайн пакетов. Также все модули из importmap в vueS3
            предзагружаются с помощью директивы
            preload.
        </div>
        <div class="col-span-1 lg:col-span-3"><el-image src="/images/f6c6095f-de2f-4a71-bf36-2fb7664178fb.png"
                :preview-src-list="['/images/f6c6095f-de2f-4a71-bf36-2fb7664178fb.png']"
                class="w-full h-auto border rounded-lg shadow-xl" />
        </div>
    </div>
    <h3>Импортирование стилей</h3>
    <p>Стили можно импортировать из раздела style с помощью директивы @import:</p>
    <highlightjs :code="ex2" language="css" class="not-prose my-6"></highlightjs>
    <dl class="mb-6">
        <template v-for="{dt, dd} in ex2dl">
            <dt class="font-bold text-slate-700">{{ dt }}</dt>
            <dd class="text-slate-500">{{ dd }}</dd>
        </template>
    </dl>
    <p>Из раздела script стили импортируются с помощью простой директивы import:</p>
    <highlightjs code='import from "url"' language="js" class="not-prose my-6"></highlightjs>
    <p>Стили импортируются только по URL к .css файлу, невозможно использовать названия и нельзя прописывать стили в
        importmap.</p>
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const ex1 = `import defaultExport from "module-name";
import * as name from "module-name";
import { export } from "module-name";
import { export as alias } from "module-name";
import { export1 , export2 } from "module-name";
import { export1 , export2 as alias2 , […] } from "module-name";
import defaultExport, { export [ , […] ] } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";
import("/module-name.js").then(module => {…}) // Динамический импорт`;

const ex1dl = [
    { dt: "defaultExport", dd: "Имя объекта, который будет ссылаться на значение экспорта по умолчанию (дефолтный экспорт) из модуля." },
    { dt: "module-name", dd: "Имя модуля для импорта. Это URL к .js файлу модуля или название модуля, указанного в importmap. Допускаются только строки с одиночными или двойными кавычками." },
    { dt: "name", dd: "Имя локального объекта, который будет использован как своего рода пространство имён, ссылающееся на импортируемые значения." },
    { dt: "export, exportN", dd: "Имена значений, которые будут импортированы." },
    { dt: "alias, aliasN", dd: "Имена, которые будут ссылаться на импортируемые значения." },
];

const ex2 = `@import url;
@import url layer;
@import url layer(layer-name);
@import url layer(layer-name) supports(supports-condition);
@import url layer(layer-name) supports(supports-condition) list-of-media-queries;
@import url layer(layer-name) list-of-media-queries;
@import url supports(supports-condition);
@import url supports(supports-condition) list-of-media-queries;
@import url list-of-media-queries;`;

const ex2dl = [
    { dt: "url", dd: "Тип <string> или <url>, представляющий местоположение импортируемого ресурса." },
    { dt: "list-of-media-queries", dd: "Список медиазапросов, разделенных запятыми, которые определяют медиазависимые условия для применения правил CSS, определенных в связанном URL. Если браузер не поддерживает ни один из этих запросов, он не загружает связанный ресурс." },
    { dt: "layer-name", dd: "Имя каскадного слоя, в который импортируется содержимое связанного ресурса." },
    { dt: "supports-condition", dd: "Указывает функцию(и), которую(ые) должен(ы) поддерживать браузер, чтобы таблица стилей была импортирована. Если браузер не соответствует условиям, указанным в supports-condition, он может не получить связанную таблицу стилей, и даже если она будет загружена по другому пути, не загрузит ее." },
];

</script>


