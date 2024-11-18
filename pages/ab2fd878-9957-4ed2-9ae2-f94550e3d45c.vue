<template>
<div class="container mx-auto" un-cloak>
  <div class="flex flex-col text-center not-prose mb-12">
    <icon :icon="the.icon" class="size-20 mx-auto"></icon>
    <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
    <el-text size="large">{{ the.description }}</el-text>
  </div>
    <el-alert title="Предотвращение FOUC" type="warning" :closable="false" show-icon>
        Используйте атрибут un-cloak для предотвращения мерцания нестилизованного содержимого.
        Подробности: <el-link href="https://unocss.dev/integrations/runtime#preventing-fouc" target="_blank">Preventing
            FOUC</el-link>.
    </el-alert>
    <br>
    <el-alert title="Сброс стилей браузера" type="info" :closable="false" show-icon>
        Стили браузера сброшены по схеме "Tailwind compat".
        Подробности: <el-link href="https://unocss.dev/guide/style-reset#tailwind-compat" target="_blank">Tailwind
            compat</el-link>.
    </el-alert>
    <el-card shadow="hover" v-for="{title, description, link, body, prose} in presets" class="my-10">
        <template #header>
            <span v-html="description"></span> Подробности: <el-link :href="link" target="_blank">{{ title }}</el-link>.
        </template>
        <el-tabs tab-position="left">
            <el-tab-pane label="Template" class="not-prose">
                <highlightjs language="html" :code="body"></highlightjs>
            </el-tab-pane>
            <el-tab-pane label="Результат" v-html="body" :class="{ 'not-prose': !prose }"></el-tab-pane>
        </el-tabs>
    </el-card>
    <el-alert title="Что почитать про атомарный CSS?" type="success" :closable="false" show-icon>
        <ul>
            <li><el-link href="https://unocss.dev/interactive" target="_blank">Интерактивная документация
                    UnoCSS</el-link></li>
            <li><el-link href="https://tailwindcss.ru/docs/utility-first" target="_blank">Документация Tailwind
                    CSS</el-link></li>
        </ul>
    </el-alert>
</div>
</template>

<script setup>
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];
const presets = [{
  title: "Uno preset",
  prose: false,
  description: "<a href='https://tailwindcss.ru' target='_blank' rel='noopener noreferrer'>Tailwind CSS</a> доступна для использования без каких-либо дополнительных настроек.",
  link: "https://unocss.dev/presets/uno",
  body: `<div class="mx-6 mb-6 p-6 max-w-sm bg-white rounded-xl shadow-lg flex items-center space-x-4">
    <div class="shrink-0">
        <div class="i-token-branded:chat size-12"></div>
    </div>
    <div>
        <div class="text-xl font-medium text-black">ChitChat</div>
        <p class="text-slate-500">У вас новое сообщение!</p>
    </div>
</div>`
}, {
  title: "Icons preset",
  prose: false,
  description: "Любая иконка из проекта <a href='https://icon-sets.iconify.design' target='_blank' rel='noopener noreferrer'>Iconify</a> доступна по первому требованию.",
  link: "https://unocss.dev/presets/icons",
  body: `<div class="flex items-center gap-x-4 text-4xl p-2 mt-4">
    <div class="i-ph:anchor-simple-thin"></div>
    <div class="i-mdi:alarm text-orange-400 hover:text-teal-400"></div>
    <div class="w-2em h-2em i-logos:vue transform transition-800 hover:rotate-180"></div>
    <div class="i-carbon:sun dark:i-carbon:moon !w-2em !h-2em"></div>
    <div class="i-twemoji:grinning-face-with-smiling-eyes hover:i-twemoji:face-with-tears-of-joy"></div>
    <div class="text-base my-auto flex"><div class="i-carbon:arrow-left my-auto mr-1"></div> Hover it</div>
</div>`
}, {
  title: "Typography preset",
  prose: true,
  description: "Красивые типографские настройки <a href='https://tailwindcss.ru/docs/typography-plugin/' target='_blank' rel='noopener noreferrer'>prose</a> для HTML.",
  link: "https://unocss.dev/presets/typography",
  body: `<article class="prose-pink lg:text-xl">
  <h1>Чесночный хлеб с сыром: что говорит нам наука</h1>
  <p>
    В течение многих лет родители поддерживали пользу для здоровья от употребления в пищу чесночного хлеба с сыром
    для своих детей, и эта еда приобрела такой культовый статус в нашей культуре,
    что дети часто наряжаются теплым, сырным хлебом на Хэллоуин.
  </p>
  <p>
    Но недавнее исследование показывает, что знаменитая закуска может быть связана
    с серией случаев бешенства, возникающих по всей стране.
  </p>
</article>`
}, {
  title: "Web Fonts preset",
  prose: true,
  description: "Динамические антиквы, геометрические гротески, рукописные шрифты, гуманистические гротески, неогротески, статические антиквы, переходные антиквы - всего 56 предустановленных качественных шрифтов",
  link: "https://unocss.dev/presets/web-fonts",
  body: `<p class="font-['Piazzolla']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Montserrat']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Marck_Script']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Open_Sans']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Roboto']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['IBM_Plex_Serif']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Merriweather']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>`
}];
</script>


