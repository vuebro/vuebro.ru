<template>
  <div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-12">
      <icon :icon="the.icon" class="size-20 mx-auto"></icon>
      <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
      <el-text size="large">{{ the.description }}</el-text>
    </div>
    <el-alert :title="t('warningHeader')" type="warning" :closable="false" show-icon>
      {{ t("warning") }}<el-tag>Ctrl+Shift+I</el-tag>
    </el-alert>
    <h3 class="text-slate-600">{{ t("header") }}</h3>
    <el-text v-html="t('info')"></el-text>
    <el-timeline class="not-prose !mt-12">
      <el-timeline-item :timestamp="`${t('step')} ${index + 1}`" placement="top"
        v-for="({ header, text, code, src, to }, index) in times">
        <el-card shadow="hover">
          <template #header><el-text tag="b">{{ header }}</el-text></template>
          <template #footer v-if="to.length"><el-text tag="b" type="info">{{ t("links") }}</el-text>
            <div class="mt-4 gap-4 flex flex-wrap"><span v-for="(link, index) in to"><el-button tag="router-link"
                  :to="`/${link}/`" :type="type[index % 5]">{{ link
                  }}</el-button></span></div>
          </template>
          <div class="grid grid-cols-1 gap-6 lg:grid-cols-8">
            <div class="col-span-1" :class="`lg:col-span-${src ? 5 : 8}`">
              <el-text v-html="text"></el-text>
              <highlightjs :code="code" v-if="code" class="my-6"></highlightjs>
            </div>
            <div class="col-span-1 lg:col-span-3" v-if="src"><el-image :src="src" :preview-src-list="[src]" v-if="src"
                class="w-full h-auto" :class="{ border: index === times.length-1 }" />
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
        info: 'The example repository is available at <a href="https://github.com/vues3/example" class="text-color-blue-500 hover:underline" target="_blank">https://github.com/vues3/example</a>, and the live example can be viewed at <a href="https://vues3.github.com/example" class="text-color-blue-500 hover:underline" target="_blank">https://vues3.github.com/example</a>',
        warningHeader: "Debugging",
        warning: "vueS3 is a serverless system and the website build process takes place in the user's browser. Therefore, the main debugging tool is the browser’s developer console, which can be opened by pressing ",
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
        header4: "Design of the Root Page",
        link42: "documentation/template",
        link43: "documentation/semantics",
        link44: "documentation/unocss",
        link45: "documentation/seo",
        description4: "The root page serves as a template common to all pages of the website. Pay attention to the <strong>&lt;router-view&gt;&lt;/router-view&gt;</strong> tag, which indicates the mounting point for the site's child pages. For more details, visit <a href='https://router.vuejs.org' class='text-color-blue-500 hover:underline' target='_blank'>https://router.vuejs.org</a>. Also, pay attention to the <strong>flat</strong> parameter in the page settings palette, which determines whether child pages will be displayed individually or all together in a flat view.",
        header5: "Adding Page 1",
        description5: "Let’s place the website banner on the first page. Note the mechanism for obtaining the ID of the current page: <strong>const {'{'} id {'}'} = defineProps([\"id\"]), pages = inject(\"pages\"), {'{'} i, title, description {'}'} = pages[id];</strong> Using this, we ultimately retrieve the title, description, and icon of the current page from the semantic array of pages.",
        header6: "Adding Page 2",
        description6: "On the second page, we will place a block with three headings and descriptions taken from the <strong>features</strong> object.",
        code6: `<template>
  <div class="container mx-auto px-4 py-24 text-center" un-cloak>
    <h3>{{ title }}</h3>
    <p class="mb-24">{{ description }}</p>
    <div class="grid grid-cols-4 gap-6 gap-y-12 lg:grid-cols-12 not-prose">
      <div class="col-span-4 flex flex-col items-center text-center" v-for="({ name, text }, index) in features">
        <div class="size-6 text-emerald-500" :class="\`i-mdi:numeric-\${index + 1}-circle-outline\`"></div>
        <h3 class="my-4 text-lg leading-6 text-slate-700">{{ name }}</h3>
        <p class="text-slate-500">{{ text }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import {'{'} inject {'}'} from "vue";
const {'{'} id {'}'} = defineProps(["id"]),
  pages = inject("pages"),
  {'{'} title, description {'}'} = pages[id],
  features = [
    {'{'}
      name: "The Simplest Website",
      text: "We create the simplest website using vueS3",
    {'}'},
    {'{'}
      name: "The Fastest Website",
      text: "We build websites on vueS3 very quickly",
    {'}'},
    {'{'}
      name: "The Most Technologically Advanced Website",
      text: "We create websites using the latest technologies",
    {'}'},
  ];
<\/script>`,
        header7: "Adding Page 3",
        description7: "Generate a dozen paragraphs of random text on the third page.",
        header8: "Result",
        description8: `The final step is to perform a <strong>commit && push</strong>, after which the live website will be accessible on GitHub Pages.
<br><br>HTML was originally designed as a simple and intuitive tool that required no additional configuration or compilation. In just 8 easy steps, you have created a website without any extra setup or compilation, while now harnessing the full reactive power of Vue.
<br><br>History repeats itself, doesn't it?
<br><br>P.S. The source code for the example is available at <a href="https://github.com/vues3/example" class="text-color-blue-500 hover:underline" target="_blank">https://github.com/vues3/example</a>, and the live example can be viewed at <a href="https://vues3.github.io/example" class="text-color-blue-500 hover:underline" target="_blank">https://vues3.github.io/example</a>`,
      },
      ru: {
        links: "Ссылки по теме",
        step: "Шаг",
        header: "Туториал по созданию простого сайта в vueS3",
        info: 'Репозиторий примера находится по адресу <a href="https://github.com/vues3/example.ru" class="text-color-blue-500 hover:underline" target="_blank">https://github.com/vues3/example.ru</a>, работающий пример: <a href="https://vues3.github.io/example.ru" class="text-color-blue-500 hover:underline" target="_blank">https://vues3.github.io/example.ru</a>',
        warningHeader: "Отладка",
        warning: "vueS3 это безсерверная система и сборка сайта происходит в браузере пользователя. Поэтому основной инструмент отладки - консоль разработчика в браузере, которая вызывается по нажатию ",
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
        header4: "Оформление корневой страницы",
        description4: "Корневая страница представляет собой шаблон общий для всех страниц сайта. Обратите внимание на таг <strong>&lt;router-view&gt;&lt;/router-view&gt;</strong>, указывающий на точку монтирования для дочерних страниц сайта. Подробности на <a href='https://vue-router-ru.netlify.app' class='text-color-blue-500 hover:underline' target='_blank'>https://vue-router-ru.netlify.app</a>. Также следует обратить внимание на параметр <strong>flat</strong> в палитре настроек страницы, который определяет, будут ли показываться дочерние страницы по отдельности, либо в плоском виде все вместе.",
        link42: "документация/шаблон",
        link43: "документация/семантика",
        link44: "документация/unocss",
        link45: "документация/seo",
        header5: "Добавление страницы 1",
        description5: "Разместим на первой странице банер сайта. Обратите внимание на механизм получения id текущей страницы <strong>const {'{'} id {'}'} = defineProps([\"id\"]), pages = inject(\"pages\"), {'{'} i, title, description {'}'} = pages[id];</strong> с помощью которого в итоге получаем заголовок, описание и иконку текущей страницы из семантического массива страниц.",
        header6: "Добавление страницы 2",
        description6: "На второй странице разместим блок с тремя заголовками и описаниями, взятыми из объекта <strong>features</strong>.",
        code6: `<template>
  <div class="container mx-auto px-4 py-24 text-center" un-cloak>
    <h3>{{ title }}</h3>
    <p class="mb-24">{{ description }}</p>
    <div class="grid grid-cols-4 gap-6 gap-y-12 lg:grid-cols-12 not-prose">
      <div class="col-span-4 flex flex-col items-center text-center" v-for="({ name, text }, index) in features">
        <div class="size-6 text-emerald-500" :class="\`i-mdi:numeric-\${index + 1}-circle-outline\`"></div>
        <h3 class="my-4 text-lg leading-6 text-slate-700">{{ name }}</h3>
        <p class="text-slate-500">{{ text }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import {'{'} inject {'}'} from "vue";
const {'{'} id {'}'} = defineProps(["id"]),
  pages = inject("pages"),
  {'{'} title, description {'}'} = pages[id],
  features = [
    {'{'}
      name: "Самый простой сайт",
      text: "Мы делаем самый простой сайт на vueS3",
    {'}'},
    {'{'}
      name: "Самый быстрый сайт",
      text: "Мы делаем сайт на vueS3 очень быстро",
    {'}'},
    {'{'}
      name: "Самый технологичный сайт",
      text: "Мы делаем сайт, используя самые современные технологии",
    {'}'},
  ];
<\/script>`,
        header7: "Добавление страницы 3",
        description7: "Генерируем дюжину абзацев случайного текста на третьей странице.",
        header8: "Результат",
        description8: `Заключительным этапом сделайте <strong>commit && push</strong>, после чего рабочий сайт будет доступен на GitHub Pages.
        <br><br>Html был задуман простым и понятным инструментом, который не требовал дополнительных настроек и компиляции.
        За 8 простых шагов вы создали сайт, без дополнительных настроек и компиляции, только теперь используя всю рективную мощь Vue.
        <br><br>История повторяется, не правда ли? 
        <br><br>P.S. Исходники примера находятся по адресу <a href="https://github.com/vues3/example.ru" class="text-color-blue-500 hover:underline" target="_blank">https://github.com/vues3/example.ru</a>, а работающий пример на <a href="https://vues3.github.io/example.ru" class="text-color-blue-500 hover:underline" target="_blank">https://vues3.github.io/example.ru</a>`,
      }
    }
  }),
  times = reactive([
    {
      header: t("header1"),
      text: t("description1"), code: "", src: "",
      to: [],
    },
    {
      header: t("header2"),
      text: t("description2"), code: "", src: "images/qstart/1.png",
      to: [t("link2")],
    },
    {
      header: t("header3"),
      text: t("description3"), code: "", src: "images/qstart/2.png",
      to: [t("link31")/*, t("link32")*/],
    },
    {
      header: t("header4"),
      text: t("description4"),
      code: `<template>
  <div class="min-h-dvh" un-cloak>
    <el-page-header :icon="AlarmClock" :content="pages[$route.name].title" :title="title" @back="$router.push('/')"
      class="sticky top-0 z-50 pa-4 border-b bg-neutral-50"></el-page-header>
    <router-view></router-view>
  </div>
  <div class="flex flex-col gap-8 items-center bg-neutral-200 pa-12 not-prose" un-cloak>
    <el-button-group>
      <el-button v-for="child in $children" tag="router-link" :to="child.to">{{ child.title }}</el-button>
    </el-button-group>
    <el-text>{{ description }}</el-text>
  </div>
</template>
<script setup>
import "https://cdn.jsdelivr.net/npm/element-plus@^2/dist/index.css";
import ElementPlus from "element-plus";
import { AlarmClock } from "@element-plus/icons-vue";
import { inject } from "vue";
window.app.use(ElementPlus);
const { id } = defineProps(["id"]),
  pages = inject("pages"),
  { title, description, $children } = pages[id];
<\/script>`,
      src: "images/qstart/3.png",
      to: [/*t("link42"), t("link43"), t("link44"), t("link45")*/],
    },
    {
      header: t("header5"),
      text: t("description5"),
      code: `<template>
  <div class="container mx-auto px-4 py-24" un-cloak>
    <el-card body-class="h-96 flex flex-col items-center justify-center text-center">
      <div :class="i" class="size-12"></div>
      <h2>{{ title }}</h2>
      <p>{{ description }}</p>
    </el-card>
  </div>
</template>
<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]),
  pages = inject("pages"),
  { i, title, description } = pages[id];
<\/script>`,
      src: "images/qstart/4.png",
      to: [/*t("link42"), t("link43"), t("link44"), t("link45")*/],
    },
    {
      header: t("header6"),
      text: t("description6"),
      code: t("code6"),
      src: "images/qstart/5.png",
      to: [/*t("link42"), t("link43"), t("link44"), t("link45")*/],
    },
    {
      header: t("header7"),
      text: t("description7"),
      code: `<template>
  <div class="container mx-auto px-4 py-24">
    <h3 class="text-center">{{ title }}</h3>
    <p class="text-center mb-12">{{ description }}</p>
    <p v-for="paragraph in text" class="text-justify">{{ paragraph }}</p>
  </div>
</template>
<script setup>
import { inject } from "vue";
import { getParagraph } from "speech-code";
const { id } = defineProps(["id"]),
  pages = inject("pages"),
  { title, description } = pages[id],
  text = Array(12).fill().map(() => getParagraph());
<\/script>`,
      src: "images/qstart/6.png",
      to: [/*t("link42"), t("link43"), t("link44"), t("link45")*/],
    },
    {
      header: t("header8"),
      text: t("description8"),
      code: "",
      language: "",
      src: "images/qstart/7.png",
      to: [],
    },
  ]);
</script>
