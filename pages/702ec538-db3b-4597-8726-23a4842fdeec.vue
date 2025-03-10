<template>
    <div class="sm:py-24 text-slate-800 overflow-hidden">
        <div class="my-24 flex justify-center">
            <icon class="text-2xl sm:text-6xl flex justify-items-center" icon="bxs:chevrons-down"></icon>
        </div>
        <h2 class="mb-3 sm:mb-6 text-2xl sm:text-5xl font-['Rubik_Glitch']">{{ t("doesnt") }}</h2>
        <h2 class="mb-3 sm:mb-6 text-2xl sm:text-5xl font-['Rubik_Glitch']">//</h2>
        <h2 class="text-2xl sm:text-5xl font-['Rubik_Glitch']" v-html="t('does')"></h2>
        <h1 class="my-12 sm:my-24 text-4xl sm:text-7xl font-['Jura'] animate__animated" v-html="t('newtech')"
            v-intersection-observer="([{ isIntersecting }]) => { anima = isIntersecting }"
            :class="{ animate__fadeInRight: anima, animate__fadeOutRight: !anima, }"></h1>
        <div class="my-24 flex justify-center">
            <icon class="text-2xl sm:text-6xl flex justify-items-center" icon="bxs:chevrons-down"></icon>
        </div>
    </div>
    <ul class="divide-y-2 divide-dashed divide-slate-800" un-cloak>
        <li class="flex items-center gap-4 px-4 py-6 flex-nowrap" v-for="{ text, icon } in features">
            <div>
                <Icon :icon="icon" class="size-12"
                </Icon>
            </div>
            <el-text size="large" v-html="text"></el-text>
        </li>
    </ul>
</template>

<script setup>
import { ref } from "vue";
import { vIntersectionObserver } from "@vueuse/components";
import { useI18n } from "vue-i18n";

const { t } = useI18n({
    messages: {
        en: {
            doesnt: "Don't do it the old way",
            does: `Let's do <span class="text-white bg-red-500">&nbsp;everything differently&nbsp;</span>`,
            newtech: 'Try a <span class="text-white bg-slate-800">&nbsp;new technology&nbsp;</span> of website development',
            rocket: "Create <a href='https://en.wikipedia.org/wiki/Static_web_page' target='_blank' class='underline hover:text-blue-800'>static websites</a> with <a href='https://vuejs.org' target='_blank' class='underline hover:text-blue-800'>Vue</a> without installing or setting up a development environment (<a href='https://nodejs.org' target='_blank' class='underline hover:text-blue-800'>Node.js</a>, <a href='https://vite.dev' target='_blank' class='underline hover:text-blue-800'>Vite</a>, etc.)",
            "building-construction": "Create <a href='https://vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>Vue single-file components</a> (also known as *.vue files, or SFC for Single File Component) without a preliminary build step",
            "racing-car": "Compilation of <a href='https://vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>Vue single-file components</a> occurs in the runtime mode directly in the browser when viewing the site, with no need for <a href='https://vuejs.org/guide/scaling-up/ssr.html' target='_blank' class='underline hover:text-blue-800'>SSR</a> (Server-Side Rendering)",
            typescript: "Of course, you can use the <a href='https://vuejs.org/guide/introduction.html#composition-api' target='_blank' class='underline hover:text-blue-800'>Composition API</a>, moreover, it can be used together with <a href='https://vuejs.org/guide/typescript/composition-api.html' target='_blank' class='underline hover:text-blue-800'>TypeScript</a>",
            "spiral-notepad": "For static pages, use the <a href='https://en.wikipedia.org/wiki/WYSIWYG' target='_blank' class='underline hover:text-blue-800'>WYSIWYG</a> mode, which doesn’t require even basic knowledge of <a href='https://en.wikipedia.org/wiki/HTML' target='_blank' class='underline hover:text-blue-800'>HTML</a>",
            "code-editor": "For editing <a href='https://vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>Vue single-file components</a>, the <a href='https://microsoft.github.io/monaco-editor' target='_blank' class='underline hover:text-blue-800'>Monaco editor</a> is used (the same one as in <a href='https://code.visualstudio.com' target='_blank' class='underline hover:text-blue-800'>Microsoft VS Code</a>) with <a href='https://volarjs.dev' target='_blank' class='underline hover:text-blue-800'>Volar.js</a> pre-installed",
            paintbrush: "Out of the box, the CSS framework <a href='https://tailwindcss.com' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a> is supported; just use <a href='https://tailwindcss.com' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a> classes without any additional configuration",
            ship: "If you need external modules, such as libraries or frameworks, you can <a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import' target='_blank' class='underline hover:text-blue-800'>import</a> them, including directly from services like <a href='https://jsdelivr.com' target='_blank' class='underline hover:text-blue-800'>jsDelivr</a> and <a href='https://unpkg.com' target='_blank' class='underline hover:text-blue-800'>UNPKG</a>",
            "floppy-disk": "You can edit the website directly on your hard drive or connect to any S3 storage",
            "globe-with-meridians": "To run your website, you'll only need any basic <a href='https://en.wikipedia.org/wiki/Web_server' target='_blank' class='underline hover:text-blue-800'>web server</a> capable of serving static pages. In the case of S3, you don't even need that, as this functionality is usually built into the storage itself",
            github: "By the way, <a href='https://docs.github.com/en/pages' target='_blank' class='underline hover:text-blue-800'>GitHub Pages</a> is also a great option for hosting your website—it works like a charm",
            "magnifying-glass-tilted-right": "Special attention is given to <a href='https://en.wikipedia.org/wiki/Search_engine_optimization' target='_blank' class='underline hover:text-blue-800'>search engine optimization</a> (SEO) mechanisms, which ensure that search bots can effectively index the site",
            "smiling-face-with-open-hands": "vueS3 is a non-commercial, <a href='https://en.wikipedia.org/wiki/Open-source_software' target='_blank' class='underline hover:text-blue-800'>open-source</a> project – feel free to explore and use it!",
        },
        ru: {
            doesnt: "Не делай по-старому",
            does: 'Давай сделаем <span class="text-white bg-red-500">&nbsp;всё по-другому&nbsp;</span>',
            newtech: 'Попробуй <span class="text-white bg-slate-800">&nbsp;новую технологию&nbsp;</span> разработки сайтов',
            rocket: "Делай <a href='https://ru.wikipedia.org/wiki/Статический_сайт' target='_blank' class='underline hover:text-blue-800'>статические сайты</a> на <a href='https://ru.vuejs.org' target='_blank' class='underline hover:text-blue-800'>Vue</a> без установки и настройки окружения разработчика (<a href='https://nodejs.org' target='_blank' class='underline hover:text-blue-800'>Node.js</a>, <a href='https://vite.dev' target='_blank' class='underline hover:text-blue-800'>Vite</a> и т.д.)",
            "building-construction": "Создавай <a href='https://ru.vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>однофайловые компоненты Vue</a> (они же файлы *.vue, сокращённо SFC, от Single File Component) без предварительного этапа сборки",
            "racing-car": "Компиляция <a href='https://ru.vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>однофайловых компонентов Vue</a> происходит в runtime режиме непосредственно в браузере при просмотре сайта, <a href='https://ru.vuejs.org/guide/scaling-up/ssr.html' target='_blank' class='underline hover:text-blue-800'>SSR</a> не требуется",
            typescript: "Конечно, можно использовать <a href='https://ru.vuejs.org/guide/introduction.html#composition-api' target='_blank' class='underline hover:text-blue-800'>Composition API</a>, более того, его можно использовать вместе с <a href='https://ru.vuejs.org/guide/typescript/composition-api.html' target='_blank' class='underline hover:text-blue-800'>TypeScript</a>",
            "spiral-notepad": "Для статичных страниц задействуй режим <a href='https://ru.wikipedia.org/wiki/WYSIWYG' target='_blank' class='underline hover:text-blue-800'>WYSIWYG</a>, он не требует даже минимальных знаний <a href='https://ru.wikipedia.org/wiki/HTML' target='_blank' class='underline hover:text-blue-800'>HTML</a>",
            "code-editor": "Для редактирования <a href='https://ru.vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>однофайловых компонентов Vue</a> применяется <a href='https://microsoft.github.io/monaco-editor' target='_blank' class='underline hover:text-blue-800'>Monaco</a> (тот же, что и в <a href='https://code.visualstudio.com' target='_blank' class='underline hover:text-blue-800'>Microsoft VS Code</a>) с предустановленным <a href='https://volarjs.dev' target='_blank' class='underline hover:text-blue-800'>Volar.js</a>",
            paintbrush: "Прямо из коробки поддерживается CSS фреймворк <a href='https://tailwindcss.ru' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a>, просто используй классы <a href='https://tailwindcss.ru' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a> без какой-либо дополнительной настройки",
            ship: "Если нужны внешние модули, такие как библиотеки или фреймворки, <a href='https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/import' target='_blank' class='underline hover:text-blue-800'>импортируй</a> их, в том числе непосредственно с таких сервисов как <a href='https://jsdelivr.com' target='_blank' class='underline hover:text-blue-800'>jsDelivr</a>, <a href='https://unpkg.com' target='_blank' class='underline hover:text-blue-800'>UNPKG</a>",
            "floppy-disk": "Можешь редактировать сайт сразу на жестком диске либо подключиться к любому хранилищу S3 (<a href='https://aws.amazon.com/ru/s3' target='_blank' class='underline hover:text-blue-800'>AWS S3</a>, <a href='https://yandex.cloud/ru/services/storage' target='_blank' class='underline hover:text-blue-800'>Yandex Object Storage</a>, <a href='https://cloud.vk.com/storage' target='_blank' class='underline hover:text-blue-800'>VK Cloud Storage</a> и т.д.)",
            "globe-with-meridians": "Для работы твоего сайта понадобится лишь любой простой <a href='https://ru.wikipedia.org/wiki/веб-сервер' target='_blank' class='underline hover:text-blue-800'>веб-сервер</a>, способный отдавать статические страницы, а в случае с S3 даже он не нужен, потому что эта возможность обычно встроена в само хранилище",
            github: "Кстати, <a href='https://docs.github.com/ru/pages' target='_blank' class='underline hover:text-blue-800'>GitHub Pages</a> тоже хороший вариант для размещения сайта, работает как часы",
            "magnifying-glass-tilted-right": "Особое внимание уделено механизмам для <a href='https://ru.wikipedia.org/wiki/поисковая_оптимизация' target='_blank' class='underline hover:text-blue-800'>поисковой оптимизации</a> (SEO), благодаря этому поисковые роботы отлично видят сайт",
            "smiling-face-with-open-hands": "vueS3 это некоммерческий проект с <a href='https://ru.wikipedia.org/wiki/Открытое_программное_обеспечение' target='_blank' class='underline hover:text-blue-800'>открытым исходным кодом</a> - открывай и пользуйся!",
        }
    }
}), features = [
    "rocket",
    "building-construction",
    "racing-car",
    "typescript",
    "spiral-notepad",
    "code-editor",
    "paintbrush",
    "ship",
    "floppy-disk",
    "globe-with-meridians",
    "github",
    "magnifying-glass-tilted-right",
    "smiling-face-with-open-hands"
].map((value) => ({ icon: `openmoji:${value}`, text: t(value) })),
    anima = ref(false);
</script>