<template>
    <div class="container mx-auto px-4" un-cloak>
        <div class="flex flex-col text-center not-prose mb-24">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <h2>{{ t("h_1") }}</h2>
        <p>{{ t("p_1") }}</p>
        <highlightjs :code="ex1" language="js" class="not-prose my-6"></highlightjs>
        <dl class="mb-6">
            <template v-for="(,key) in messages.en.ex1dl">
                <dt class="font-bold text-slate-700">{{ key }}</dt>
                <dd class="text-slate-500">{{ t(`ex1dl.${key}`) }}</dd>
            </template>
        </dl>
        <h3>{{ t("h_2") }}</h3>
        <p>{{ t("p2_1") }}<a href="https://npmjs.com" target="_blank" rel="noopener noreferrer">npm</a>{{ t("p2_2") }}
        </p>
        <ul>
            <li><a href="https://unpkg.com" target="_blank" rel="noopener noreferrer">unpkg.com</a></li>
            <li><a href="https://jsdelivr.com" target="_blank" rel="noopener noreferrer">jsdelivr.com</a></li>
        </ul>
        <p>{{ t("p3") }}</p>
        <ul>
            <li><a href="https://esm.sh" target="_blank" rel="noopener noreferrer">esm.sh</a></li>
            <li><a href="https://esm.run" target="_blank" rel="noopener noreferrer">esm.run</a></li>
        </ul>
        <p>{{ t("p4") }}: <router-link :to="`/${t('link4')}/`">{{ t("link4") }}</router-link></p>
        <h3>{{ t("h3") }}</h3>
        <div class="grid grid-cols-1 gap-6 lg:grid-cols-8">
            <div class="col-span-1 lg:col-span-5 text-justify">{{ t("p5") }}</div>
            <div class="col-span-1 lg:col-span-3"><el-image src="/images/qstart/2.png"
                    :preview-src-list="['/images/qstart/2.png']"
                    class="w-full h-auto" />
            </div>
        </div>
        <h2>{{ t("h4") }}</h2>
        <p>{{ t("p6") }}:</p>
        <highlightjs :code="ex2" language="css" class="not-prose my-6"></highlightjs>
        <dl class="mb-6">
            <template v-for="(,key) in messages.en.ex2dl">
                <dt class="font-bold text-slate-700">{{ key }}</dt>
                <dd class="text-slate-500">{{ t(`ex2dl.${key}`) }}</dd>
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

<script setup vapor>
import { inject } from "vue";
import { useI18n } from "vue-i18n";
import { ArrowLeft, ArrowRight } from "@element-plus/icons-vue";

const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

const messages = {
    en: {
        h_1: "Importing Modules",
        p_1: "The static import declaration is used to import read-only live bindings which are exported by another module.",
        ex1dl: {
            "defaultExport": "Name that will refer to the default export from the module. Must be a valid JavaScript identifier.",
            "module-name": "Module name for import. This is either the URL to the module's .js file or the name of the module specified in the import map. Only strings with single or double quotes are allowed.",
            "name": "Name of the module object that will be used as a kind of namespace when referring to the imports. Must be a valid JavaScript identifier.",
            "exportN": "Name of the exports to be imported. The name can be either an identifier or a string literal, depending on what module-name declares to export. If it is a string literal, it must be aliased to a valid identifier.",
            "aliasN": "Names that will refer to the named imports. Must be a valid JavaScript identifier.",
        },
        h_2: "Network Package Sources",
        p2_1: "Online access to all packages provided through the ",
        p2_2: " package manager can be obtained via web services such as:",
        p3: "In modern packages, an ESM module file for integration is usually already included. If, for some reason, the package does not contain an ESM module, you can use services that will build the module for you from the package's source code:",
        p4: "Examples of Connecting Modules from Popular Libraries and Frameworks to vueS3",
        link4: "modules",
        h3: "Using `importmap`",
        p5: "To add a module to the 'importmap,' use the tool from the dropdown menu in the upper right corner of the main vueS3 window. The 'importmap' allows you to use names when importing modules, which is particularly useful when names are used in imports from online package modules. Additionally, all modules from the 'importmap' in vueS3 are preloaded using the `preload` directive.",
        h4: "Importing Styles",
        p6: "Styles can be imported from the `style` section using the {'@'}import directive",
        ex2dl: {
            "url": "Is a <string> or a <url> type representing the location of the resource to import.",
            "list-of-media-queries": "Is a comma-separated list of media queries, which specify the media-dependent conditions for applying the CSS rules defined in the linked URL. If the browser does not support any of these queries, it does not load the linked resource.",
            "layer-name": "Is the name of a cascade layer into which the contents of the linked resource are imported.",
            "supports-condition": "Indicates the feature(s) that the browser must support in order for the stylesheet to be imported. If the browser does not conform to the conditions specified in the supports-condition, it may not fetch the linked stylesheet, and even if downloaded through some other path, will not load it.",
        },
    },
    ru: {
        h_1: "Импортирование модулей",
        p_1: "Инструкция import используется для импорта ссылок на значения, экспортированные из внешнего модуля.",
        ex1dl: {
            "defaultExport": "Имя объекта, который будет ссылаться на значение экспорта по умолчанию (дефолтный экспорт) из модуля.",
            "module-name": "Имя модуля для импорта. Это URL к .js файлу модуля или название модуля, указанного в importmap. Допускаются только строки с одиночными или двойными кавычками.",
            "name": "Имя локального объекта, который будет использован как своего рода пространство имён, ссылающееся на импортируемые значения.",
            "exportN": "Имена значений, которые будут импортированы.",
            "aliasN": "Имена, которые будут ссылаться на импортируемые значения.",
        },
        h_2: "Сетевые источники пакетов",
        p2_1: "Онлайн доступ ко всем пакетам, предоставляемым через пакетный менеджер ",
        p2_2: " можно получить через веб сервисы, такие как:",
        p3: "В современных пакетах обычно уже присутствует файл esm модуля для подключения. Если по какой-либо причине в пакете нет esm модуля, то можно воспользоваться сервисами, которые соберут для вас модуль из исходников пакета:",
        p4: "Примеры подключения модулей популярных библиотек и фреймворков к vueS3",
        link4: "модули",
        h3: "Использование importmap",
        p5: "Для добавления модуля в importmap воспользуйтесь инструментом из выпадающего меню в правом верхнем углу основного окна vueS3. Importmap дает возможность использовать имена при импортировании модулей, что полезно, если имена используются при импортировании в модулях из онлайн пакетов. Также все модули из importmap в vueS3 предзагружаются с помощью директивы preload.",
        h4: "Импортирование стилей",
        p6: "Стили можно импортировать из раздела style с помощью директивы {'@'}import",
        ex2dl: {
            "url": "Тип <string> или <url>, представляющий местоположение импортируемого ресурса.",
            "list-of-media-queries": "Список медиазапросов, разделенных запятыми, которые определяют медиазависимые условия для применения правил CSS, определенных в связанном URL. Если браузер не поддерживает ни один из этих запросов, он не загружает связанный ресурс.",
            "layer-name": "Имя каскадного слоя, в который импортируется содержимое связанного ресурса.",
            "supports-condition": "Указывает функцию(и), которую(ые) должен(ы) поддерживать браузер, чтобы таблица стилей была импортирована. Если браузер не соответствует условиям, указанным в supports-condition, он может не получить связанную таблицу стилей, и даже если она будет загружена по другому пути, не загрузит ее.",
        },
    }
},
    { t } = useI18n({ messages });

const ex1 = `import defaultExport from "module-name";
import * as name from "module-name";
import { export1 } from "module-name";
import { export1 as alias1 } from "module-name";
import { default as alias } from "module-name";
import { export1, export2 } from "module-name";
import { export1, export2 as alias2, /* … */ } from "module-name";
import { "string name" as alias } from "module-name";
import defaultExport, { export1, /* … */ } from "module-name";
import defaultExport, * as name from "module-name";
import "module-name";`;

const ex2 = `@import url;
@import url layer;
@import url layer(layer-name);
@import url layer(layer-name) supports(supports-condition);
@import url layer(layer-name) supports(supports-condition) list-of-media-queries;
@import url layer(layer-name) list-of-media-queries;
@import url supports(supports-condition);
@import url supports(supports-condition) list-of-media-queries;
@import url list-of-media-queries;`;
</script>
