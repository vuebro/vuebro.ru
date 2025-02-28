<template>
    <div class="sm:py-24 font-light antialiased [&>*]:font-[Helvetica_Neue,Helvetica,Arial,sans-serif] text-slate-800">
        <div class="my-24 flex justify-center"><icon class="text-2xl sm:text-6xl flex justify-items-center" icon="bxs:chevrons-down"></icon></div>
        <h2 class="mb-6 text-2xl sm:text-5xl">{{ doesnt }}</h2>
        <h2 class="mb-6 text-2xl sm:text-5xl font-bold">{{ separator }}</h2>
        <h2 class="text-2xl sm:text-5xl" v-html="does"></h2>
        <h1 class="sm:my-24 text-3xl sm:text-7xl">Попробуй <span class="text-white bg-slate-800 italic">&nbsp;новую технологию&nbsp;</span> разработки сайтов</h1>
        <div class="my-24 flex justify-center"><icon class="text-2xl sm:text-6xl flex justify-items-center" icon="bxs:chevrons-down"></icon></div>
    </div>
    <ul class="divide-y-2 divide-dashed divide-slate-800" un-cloak>
        <li class="flex items-center gap-4 px-4 py-6 flex-nowrap" v-for="{ text, icon } in features">
            <div>
                <Icon :icon="icon" class="size-12" />
            </div>
            <el-text size="large" v-html="text"></el-text>
        </li>
    </ul>
</template>

<script setup>
const features = [
        { icon: "openmoji:rocket", text: "Делай <a href='https://ru.wikipedia.org/wiki/Статический_сайт' target='_blank' class='underline hover:text-blue-800'>статические сайты</a> на <a href='https://ru.vuejs.org' target='_blank' class='underline hover:text-blue-800'>Vue</a> без установки и настройки окружения разработчика (<a href='https://nodejs.org' target='_blank' class='underline hover:text-blue-800'>Node.js</a>, <a href='https://vite.dev' target='_blank' class='underline hover:text-blue-800'>Vite</a> и т.д.)" },
        { icon: "openmoji:building-construction", text: "Создавай <a href='https://ru.vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>однофайловые компоненты Vue</a> (они же файлы *.vue, сокращённо SFC, от Single File Component) без предварительного этапа сборки" },
        { icon: "openmoji:racing-car", text: "Компиляция <a href='https://ru.vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>однофайловых компонентов Vue</a> происходит в runtime режиме непосредственно в браузере при просмотре сайта, <a href='https://ru.vuejs.org/guide/scaling-up/ssr.html' target='_blank' class='underline hover:text-blue-800'>SSR</a> не требуется" },
        { icon: "openmoji:typescript", text: "Конечно, можно использовать <a href='https://ru.vuejs.org/guide/introduction.html#composition-api' target='_blank' class='underline hover:text-blue-800'>Composition API</a>, более того, его можно использовать вместе с <a href='https://ru.vuejs.org/guide/typescript/composition-api.html' target='_blank' class='underline hover:text-blue-800'>TypeScript</a>" },
        { icon: "openmoji:spiral-notepad", text: "Для статичных страниц задействуй режим <a href='https://ru.wikipedia.org/wiki/WYSIWYG' target='_blank' class='underline hover:text-blue-800'>WYSIWYG</a>, он не требует даже минимальных знаний <a href='https://ru.wikipedia.org/wiki/HTML' target='_blank' class='underline hover:text-blue-800'>HTML</a>" },
        { icon: "openmoji:code-editor", text: "Для редактирования <a href='https://ru.vuejs.org/guide/scaling-up/sfc.html' target='_blank' class='underline hover:text-blue-800'>однофайловых компонентов Vue</a> применяется <a href='https://microsoft.github.io/monaco-editor' target='_blank' class='underline hover:text-blue-800'>Monaco</a> (тот же, что и в <a href='https://code.visualstudio.com' target='_blank' class='underline hover:text-blue-800'>Microsoft VS Code</a>) с предустановленным <a href='https://volarjs.dev' target='_blank' class='underline hover:text-blue-800'>Volar.js</a>" },
        { icon: "openmoji:paintbrush", text: "Прямо из коробки поддерживается CSS фреймворк <a href='https://tailwindcss.ru' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a>, просто используй классы <a href='https://tailwindcss.ru' target='_blank' class='underline hover:text-blue-800'>Tailwind CSS</a> без какой-либо дополнительной настройки" },
        { icon: "openmoji:ship", text: "Если нужны внешние модули, такие как библиотеки или фреймворки, <a href='https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/import' target='_blank' class='underline hover:text-blue-800'>импортируй</a> их, в том числе непосредственно с таких сервисов как <a href='https://jsdelivr.com' target='_blank' class='underline hover:text-blue-800'>jsDelivr</a>, <a href='https://unpkg.com' target='_blank' class='underline hover:text-blue-800'>UNPKG</a>" },
        { icon: "openmoji:floppy-disk", text: "Можешь редактировать сайт сразу на жестком диске либо подключиться к любому хранилищу S3 (<a href='https://aws.amazon.com/ru/s3' target='_blank' class='underline hover:text-blue-800'>AWS S3</a>, <a href='https://yandex.cloud/ru/services/storage' target='_blank' class='underline hover:text-blue-800'>Yandex Object Storage</a>, <a href='https://cloud.vk.com/storage' target='_blank' class='underline hover:text-blue-800'>VK Cloud Storage</a> и т.д.)" },
        { icon: "openmoji:globe-with-meridians", text: "Для работы твоего сайта понадобится лишь любой простой <a href='https://ru.wikipedia.org/wiki/веб-сервер' target='_blank' class='underline hover:text-blue-800'>веб-сервер</a>, способный отдавать статические страницы, а в случае с S3 даже он не нужен, потому что эта возможность обычно встроена в само хранилище" },
        { icon: "openmoji:github", text: "Кстати, <a href='https://docs.github.com/ru/pages' target='_blank' class='underline hover:text-blue-800'>GitHub Pages</a> тоже хороший вариант для размещения сайта, работает как часы" },
        { icon: "openmoji:magnifying-glass-tilted-right", text: "Особое внимание уделено механизмам для <a href='https://ru.wikipedia.org/wiki/поисковая_оптимизация' target='_blank' class='underline hover:text-blue-800'>поисковой оптимизации</a> (SEO), благодаря этому поисковые роботы отлично видят сайт" },
        { icon: "openmoji:smiling-face-with-open-hands", text: "vueS3 это некоммерческий проект с <a href='https://ru.wikipedia.org/wiki/Открытое_программное_обеспечение' target='_blank' class='underline hover:text-blue-800'>открытым исходным кодом</a> - открывай и пользуйся!" },
    ],
    doesnt = "Не делай по-старому",
    separator = "//",
    does = 'Давай сделаем <span class="text-white bg-red-500 italic">&nbsp;всё по-другому&nbsp;</span>';
</script>