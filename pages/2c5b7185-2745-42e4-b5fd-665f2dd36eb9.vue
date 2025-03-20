<template>
    <div class="container mx-auto px-4" un-cloak>
        <div class="flex flex-col text-center not-prose mb-12">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <el-alert :title="t('alertHeader')" type="success" :closable="false" show-icon>
            {{ t("alert") }}<el-tag>Ctrl+Shift+I</el-tag>.
        </el-alert>
        <h3 class="text-slate-600">{{ t("header") }}</h3>
        <el-timeline class="not-prose !mt-12">
            <el-timeline-item :timestamp="`${t('step')} ${index + 1}`" placement="top"
                v-for="({ header, description, to }, index) in times">
                <el-card shadow="hover">
                    <template #header><el-text tag="b">{{ header }}</el-text></template>
                    <template #footer v-if="to.length"><el-text tag="b" type="info">{{ t("links") }}</el-text>
                        <div class="mt-4 gap-4 flex flex-wrap"><span v-for="(link, index) in to"><el-button
                                    tag="router-link" :to="`/${link}/`" :type="type[index % 5]">{{ link
                                    }}</el-button></span></div>
                    </template>
                    <div class="grid grid-cols-1 gap-6 lg:grid-cols-8"
                        v-for="({ text, code, language, src }, index) in description">
                        <el-divider class="col-span-1 lg:col-span-8 !mt-10" v-if="index">⭐</el-divider>
                        <div class="col-span-1" :class="`lg:col-span-${src ? 5 : 8}`">
                            <el-text v-html="text"></el-text>
                            <highlightjs :language="language" :code="code" v-if="code" class="my-6"></highlightjs>
                        </div>
                        <div class="col-span-1 lg:col-span-3" v-if="src"><el-image :src="src" :preview-src-list="[src]"
                                v-if="src" class="w-full h-auto border rounded-lg shadow-xl" />
                        </div>
                    </div>
                </el-card>
            </el-timeline-item>
        </el-timeline>
    </div>
</template>

<script setup>
import { inject, reactive } from "vue";
import { useI18n } from "vue-i18n";
const { id } = defineProps(["id"]),
    pages = inject("pages"),
    the = pages[id],
    type = ['primary', 'success', 'info', 'warning', 'danger'],
    { t } = useI18n({
        messages: {
            en: {
                links: "Related Links",
                step: "Step",
                header: "Tutorial for Creating a Simple Website in vueS3",
                alertHeader: "Debugging",
                alert: "vueS3 is a serverless system where the website build process takes place in the user's browser. Therefore, the main debugging tool is the browser’s developer console, which can be opened by pressing ",
                header1: "Setting Up GitHub Pages",
                description1: 'Follow the instructions at <a href="https://pages.github.com" class="text-color-blue-500 hover:underline" target="_blank">https://pages.github.com</a>, to create a repository and set up GitHub Pages.',
                header2: "Getting Started with the vueS3 Application",
                description2: 'Open <a href="https://vues3.github.io/vues3" class="text-color-blue-500 hover:underline" target="_blank">https://vues3.github.io/vues3</a> in any Chrome-based browser, as they are capable of working with the file system, or download the application for your operating system. Click the "OPEN..." button and select the directory where the repository was previously cloned.',
                link2: "download",
                header3: "Connecting External Modules",
                description3: `In the upper right corner, click on the menu icon and select 'Import Map'. In the window that appears, add the external modules that will be used for the website.
<br><br><table class="border-collapse border border-slate-400">
    <tr class="*:border *:border-slate-300 *:pa-1">
        <td>element-plus</td>
        <td>https://cdn.jsdelivr.net/npm/element-plus{'@'}^2/dist/index.full.min.mjs</td>
    </tr>
    <tr class="*:border *:border-slate-300 *:pa-1">
        <td>{'@'}element-plus/icons-vue</td>
        <td>https://cdn.jsdelivr.net/npm/{'@'}element-plus/icons-vue{'@'}^2/dist/index.min.js</td>
    </tr>
    <tr class="*:border *:border-slate-300 *:pa-1">    
        <td>speech-code</td>
        <td>https://cdn.jsdelivr.net/npm/speech-code{'@'}^2/index.js</td>
    </tr>
</table>`,
link31: "modules",
link32: "documentation/modules",
            },
            ru: {
                links: "Ссылки по теме",
                step: "Шаг",
                header: "Туториал по созданию простого сайта в vueS3",
                alertHeader: "Отладка",
                alert: "vueS3 это безсерверная система, в которой сборка сайта происходит в браузере пользователя. Поэтому основной инструмент отладки - консоль разработчика в браузере, которая вызывается по нажатию ",
                header1: "Настройка GitHub Pages",
                description1: 'Следуя указаниям инструкции <a href="https://pages.github.com" class="text-color-blue-500 hover:underline" target="_blank">https://pages.github.com</a>, создайте репозиторий и настройте GitHub Pages.',
                header2: "Начало работы с приложением vueS3",
                description2: 'Откройте <a href="https://run.vues3.ru" class="text-color-blue-500 hover:underline" target="_blank">https://run.vues3.ru</a> в любом браузере на базе хрома, они умеют работать с файловой системой, либо загрузите приложение для вашей оперционной системы. Нажмите на кнопку "ОТКРЫТЬ..." и выберите директорию, в которую ранее был склонирован репозиторий.',
                link2: "загрузка",
                header3: "Подключение внешних модулей",
                description3: `В правом верхнем углу нажмите на пиктограмму меню и выберите пункт "Import Map". В открывшемся окне добавьте внешние модули, которые будут использованы для работы сайта:
<br><br><table class="border-collapse border border-slate-400">
    <tr class="*:border *:border-slate-300 *:pa-1">
        <td>element-plus</td>
        <td>https://cdn.jsdelivr.net/npm/element-plus{'@'}^2/dist/index.full.min.mjs</td>
    </tr>
    <tr class="*:border *:border-slate-300 *:pa-1">
        <td>{'@'}element-plus/icons-vue</td>
        <td>https://cdn.jsdelivr.net/npm/{'@'}element-plus/icons-vue{'@'}^2/dist/index.min.js</td>
    </tr>
    <tr class="*:border *:border-slate-300 *:pa-1">    
        <td>speech-code</td>
        <td>https://cdn.jsdelivr.net/npm/speech-code{'@'}^2/index.js</td>
    </tr>
</table>`,
link31: "модули",
link32: "документация/модули",
            }
        }
    }),
    times = reactive([
        {
            header: t("header1"),
            description: [{ text: t("description1"), code: "", language: "", src: "" }],
            to: [],
        },
        {
            header: t("header2"),
            description: [{ text: t("description2"), code: "", language: "", src: "images/74c24adb-45ef-4225-8f8c-7f14bcc56864.png" }],
            to: [t("link2")],
        },
        {
            header: t("header3"),
            description: [{text: t("description3"), code: "", language: "", src: "images/f6c6095f-de2f-4a71-bf36-2fb7664178fb.png"}],
            to: [t("link31"), t("link32")],
        },
        {
            header: "Оформить корневую страницу",
            description: [{
                text: `Первым делом, сверяемся с документацией фреймворка и добавляем его к приложению vue.
            Делается это один раз, а потому как фреймворк будем использовать на всех страницах, подключаем его прямиком на корневой странице.`,
                code: `/** Импортируются стили фреймворка element-plus */
import "https://unpkg.com/element-plus@^2/dist/index.css";
/** Импортируется исполняемая часть фреймворка element-plus */
import ElementPlus from "element-plus";
/** Импортируеся иконка будильника */
import { AlarmClock } from "@element-plus/icons-vue";
/**  Фреймворк element-plus регистрируется в приложении vue */
window.app.use(ElementPlus.default);`,
                language: "js",
                src: "images/fa14b048-2a28-4e55-a47a-2265ff99df2e.png",
            }, {
                text: `Если на странице понадобилась семантика страниц, чаще всего названия страниц, описания, их иконки, то необходимо эту семантику к странице подключить.
            Делать это нужно для каждой страницы, где понадобится семантика. Ну, и конечно, не забываем прописать заголовок корневой страницы: "Быстрый старт"
            и её описание: "Быстрый старт в vueS3 с минимальным шагом в 5 минут", в меню страницы в правой части экрана vueS3.`,
                code: `/** Импортируется вычислитель и инжектор */
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
const sel = computed(() => pages[selId.value]);`,
                language: "js",
                src: "images/5420ee83-a659-437e-b899-382f7a00bdb7.png",
            }, {
                text: `Добавляем шаблон корневой страницы. Здесь следует обратить внимание на то, что шаблон корневой страницы является базовым и будет показываться на всех других страницах.
            Так что если вам нужен "заголовок" или "подвал сайта", одинаковый для всех страниц, отличная идея добавить их в шаблон корневой страницы.
            Ну а все остальные страницы из дерева сайта будут отображаться там, где будет установлен таг роутера vue - <router-view />.
            Также обратите внимание на то, что по умолчанию подключены классы tailwind css, которые можно использовать без каких-либо дополнительных настроек.`,
                code: `<!--
Контейнер минимальной высотой в высоту экрана.
Нужен для того чтобы при загрузке на экране не мелькал футер.
-->
<div class="min-h-dvh" un-cloak>
  <!-- Плашка вверху страницы -->
  <el-page-header :icon="AlarmClock" :content="sel.title" :title="the.title" @back="$router.push('/')"
    class="sticky top-0 z-50 pa-4 border-b bg-neutral-50" />
  <!-- Вьювер для загрузки выбранных страниц из дерева -->
  <router-view></router-view>
</div>
<!-- Футер -->
<div class="flex flex-col gap-8 items-center bg-neutral-200 pa-12 not-prose" un-cloak>
  <!-- Меню по дочерним объектам корневой страницы -->
  <el-button-group><el-button v-for="{ title, to } in the.$children" tag="router-link" :to="to">{{ title
      }}</el-button></el-button-group>
  <!-- Отображение описания корневой страницы в футере -->
  <el-text>{{ the.description }}</el-text>
</div>`,
                language: "xml",
                src: "images/83e2ec96-c361-4bc4-8e1f-2853d5b39687.png",
            }],
            to: ["документация/модули", "документация/шаблон", "документация/семантика", "документация/unocss", "документация/seo"],
        },
        {
            header: "Добавить страницу 1",
            description: [{
                text: `Инжектируем семантику сайта на также как на корневую страницу. Не забываем прописать заголовок корневой страницы: "Главный заголовок сайта"
            и её описание: "Основное описание сайта", а также иконку "mdi:alarm", в меню страницы в правой части экрана vueS3.`,
                code: `/** Импортируется инжектор */
import { inject } from "vue";
/** Подключение id страницы из props */
const { id } = defineProps(["id"]);
/** Инжектирование ассоциативного массива семантических объектов страниц */
const pages = inject("pages");
/** Получение семантического объекта текущей страницы */
const the = pages[id];`,
                language: "js",
                src: "images/5dee68c0-894a-4538-9acf-bafc7634cc02.png",
            }, {
                text: `Делаем большой баннер с выводом семантики текущей страницы: иконки, названия и описания.`,
                code: `<!-- Адаптивный контейнер с отступами -->
<div class="container mx-auto px-4 py-24" un-cloak>
  <!-- Карточка с центрированием содежимого -->
  <el-card body-class="h-96 flex flex-col items-center justify-center text-center">
    <!-- Отображение иконки текущей страницы -->
    <div :class="the.i" class="size-12"></div>
    <!-- Отображение заголовка текущей страницы -->
    <h2>{{ the.title }}</h2>
    <!-- Отображение описания текущей страницы -->
    <p>{{ the.description }}</p>
  </el-card>
</div>`,
                language: "xml",
                src: "images/8856c274-d6ba-4ed3-92ef-b88447b6076d.png",
            }],
            to: ["документация/шаблон", "документация/семантика", "документация/unocss", "документация/seo"],
        },
        {
            header: "Добавить страницу 2",
            description: [{
                text: `Инжектируем семантику сайта на также как на корневую страницу. Не забываем прописать заголовок корневой страницы: "Чем мы заняты"
            и её описание: "Мы делаем первый шаг к созданию сайта на vueS3", в меню страницы в правой части экрана vueS3.`,
                code: `/** Импортируется инжектор */
import { inject } from "vue";
/** Подключение id страницы из props */
const { id } = defineProps(["id"]);
/** Инжектирование ассоциативного массива семантических объектов страниц */
const pages = inject("pages");
/** Получение семантического объекта текущей страницы */
const the = pages[id];`,
                language: "js",
                src: "images/ccd0d9af-5e06-41ec-879e-cf56fd31bae2.png",
            }, {
                text: `Теперь добавим массив объектов с описанием карточек, которые будут выведены на второй странице.`,
                code: `/** Массив содержимого карточек */
const features = [
    {
        name: "Самый простой сайт",
        description: "Мы делаем самый простой сайт на vueS3"
    },
    {
        name: "Самый быстрый сайт",
        description: "Мы делаем сайт на vueS3 очень быстро"
    },
    {
        name: "Самый технологичный сайт",
        description: "Мы делаем сайт, используя самые современные технологии"
    }
]`,
                language: "js",
                src: "images/2fe0f752-40aa-4b6e-92b5-f3fb9057864b.png",
            }, {
                text: `Ну а следом добавим на страницу шаблон, который выводит карточки на основе уже созданного массива.`,
                code: `<!-- Адаптивный контейнер с отступами -->
<div class="container mx-auto px-4 py-24 text-center" un-cloak>
    <!-- Отображение заголовка текущей страницы -->
    <h3>{{ the.title }}</h3>
    <!-- Отображение описания текущей страницы -->
    <p class="mb-24">{{ the.description }}</p>
    <!-- Адаптивная сетка для отображения карточек -->
    <div class="grid grid-cols-4 gap-6 gap-y-12 lg:grid-cols-12 not-prose">
        <!-- Вывод карточек из массива содержимого -->
        <div class="col-span-4 flex flex-col items-center text-center" v-for="({name, description}, index) in features">
            <!-- Иконка номера карточки -->
            <div class="size-6 text-emerald-500 " :class="\`i-mdi:numeric-\${index + 1}-circle-outline\`"></div>
            <!-- Заголовок карточки -->
            <h3 class="my-4 text-lg leading-6 text-slate-700">{{ name }}</h3>
            <!-- Описание карточки -->
            <p class="text-slate-500">{{ description }}</p>
        </div>
    </div>
</div>`,
                language: "xml",
                src: "images/ebf281eb-8f86-449f-a106-46c1d42d1651.png",
            }],
            to: ["документация/шаблон", "документация/семантика", "документация/unocss", "документация/seo"],
        },
        {
            header: "Добавить страницу 3",
            description: [{
                text: `Инжектируем семантику сайта на также как на корневую страницу. Не забываем прописать заголовок корневой страницы: "Основной текст"
            и её описание: "Текст был сгенерирован случайным образом", в меню страницы в правой части экрана vueS3.`,
                code: `/** Импортируется инжектор */
import { inject } from "vue";
/** Подключение id страницы из props */
const { id } = defineProps(["id"]);
/** Инжектирование ассоциативного массива семантических объектов страниц */
const pages = inject("pages");
/** Получение семантического объекта текущей страницы */
const the = pages[id];`,
                language: "js",
                src: "images/56efb35d-478c-49ed-a323-ead01e862685.png",
            }, {
                text: `Подключаем библиотеку для генерации случайного текста и сразу же используем её, получая на выходе 12 бессмысленных абзацев.`,
                code: `/** Импортируется генератор случайного текста */
import { getParagraph } from "https://unpkg.com/speech-code@^2/index.js";
/** Массив из 12 абзацев случайного текста */
const text = Array(12).fill().map(() => getParagraph());`,
                language: "js",
                src: "images/2f63934f-8672-4a02-a746-91f5c5a88609.png",
            }, {
                text: `В завершении выводим бессмысленный текст на экран с помощью простого шаблона.`,
                code: `<!-- Адаптивный контейнер с отступами -->
<div class="container mx-auto px-4 py-24">
    <!-- Отображение заголовка текущей страницы -->
    <h3 class="text-center">{{ the.title }}</h3>
    <!-- Отображение описания текущей страницы -->
    <p class="text-center mb-12">{{ the.description }}</p>
    <!--  Вывод массива абзацев случайного текста -->
    <p v-for="paragraph in text" class="text-justify">{{ paragraph }}</p>
</div>`,
                language: "xml",
                src: "images/a4e1d98f-6c96-40f5-b097-274166c237c1.png",
            }],
            to: ["документация/шаблон", "документация/семантика", "документация/unocss", "документация/seo"],
        },
        {
            header: "Результат",
            description: [{
                text: `В результате, за 45 минут, или скорее всего еще быстрее, можно без проблем сделать простой сайт, который уже доступен в сети интернет.
            Обратите внимание, что страницы выводятся на одном экране. При необходимости, можно сделать классический вывод по одной странице на экран.
            Для этого, у родительской страницы (в нашем примере это будет корневая страница), снимите галочку у параметра alone, в меню страницы в правой части экрана vueS3.`,
                code: "",
                language: "",
                src: "images/322d90f0-2abe-4b0b-9ae1-89c73b5ab1d6.png",
            }],
            to: [],
        },
    ]);
</script>
