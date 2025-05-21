<template>
  <div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-24">
      <icon :icon="the.icon" class="size-20 mx-auto"></icon>
      <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
      <el-text size="large">{{ the.description }}</el-text>
    </div>
    <el-alert :title="t('title1')" type="warning" :closable="false" show-icon>
      {{ t("desc1") }}
      {{ t("details") }}: <el-button tag="a" href="https://unocss.dev/integrations/runtime#preventing-fouc"
        target="_blank" rel="noopener noreferrer">Preventing
        FOUC</el-button>
    </el-alert>
    <br>
    <el-alert :title="t('title2')" type="info" :closable="false" show-icon>
      {{ t("desc2") }}
      {{ t("details") }}: <el-button tag="a" href="https://unocss.dev/guide/style-reset#tailwind-compat" target="_blank"
        rel="noopener noreferrer">Tailwind
        compat</el-button>
    </el-alert>
    <el-card shadow="hover" v-for="({ prose }, i) in messages.en.presets" class="my-10">
      <template #header>
        <el-text><span v-html="t(`presets[${i}].description`)"></span> {{ t("details") }}:</el-text> <el-button
          :href="t(`presets[${i}].link`)" target="_blank" tag="a" rel="noopener noreferrer">{{
            t(`presets[${i}].title`) }}</el-button>
      </template>
      <el-tabs tab-position="left">
        <el-tab-pane label="Template">
          <highlightjs language="html" :code="t(`presets[${i}].body`)"></highlightjs>
        </el-tab-pane>
        <el-tab-pane :label="t('result')" v-html="t(`presets[${i}].body`)" :class="{ 'prose': prose }"></el-tab-pane>
      </el-tabs>
    </el-card>
    <div class="mb-10"><el-alert type="info" :closable="false" :title="t('title4')" effect="dark"><img
          src="images/fonts.png"></el-alert></div>
    <el-alert :title="t('title32')" type="success" :closable="false" show-icon>
      <ul>
        <li><el-link class="hover:no-underline" href="https://unocss.dev/interactive" target="_blank">{{ t("subtitle21")
        }}</el-link></li>
        <li><el-link class="hover:no-underline" :href="t('href22')" target="_blank">{{ t("subtitle22") }}</el-link></li>
      </ul>
    </el-alert>
    <div class="not-prose flex mt-48">
      <el-button-group class="mx-auto" size="large">
        <el-button class="my-1" type="primary" :icon="ArrowLeft" :to="the.$prev.to" v-if="the.$prev"
          tag="router-link">{{
            the.$prev.header }}</el-button>
        <el-button class="my-1" type="primary" v-if="the.$next" :to="the.$next.to" tag="router-link">{{ the.$next.header
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
    title4: "Before use, add the font name via the font adding dialog box",
    result: "Result",
    title1: "Preventing FOUC",
    title2: "Browser Style Reset",
    title32: "What to Read About Atomic CSS?",
    desc1: "Use the \"un-cloak\" attribute to prevent the flickering of unstyled content.",
    desc2: "Browser styles are reset according to the \"Tailwind compat\" scheme.",
    details: "For more details, see",
    subtitle21: "UnoCSS Interactive Docs",
    subtitle22: "Tailwind CSS Documentation",
    href22: "https://tailwindcss.com/docs/styling-with-utility-classes",
    presets: [{
      title: "Wind4 preset",
      prose: false,
      description: "<a href='https://tailwindcss.com' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>Tailwind CSS</a> is available for use without any additional configuration.",
      link: "https://unocss.dev/presets/wind4",
      body: `<div class="mx-6 mb-6 p-6 max-w-sm bg-white rounded-xl shadow-lg flex items-center space-x-4">
    <div class="shrink-0">
        <div class="i-token-branded:chat size-12"></div>
    </div>
    <div>
        <div class="text-xl font-medium text-black">ChitChat</div>
        <p class="text-slate-500">You have a new message!</p>
    </div>
</div>`
    }, {
      title: "Icons preset",
      prose: false,
      description: "Any icon from the <a href='https://icon-sets.iconify.design' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>Iconify</a> project is available on demand.",
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
      description: "Beautiful typographic settings for HTML using <a href='https://tailwindcss.com/docs/typography-plugin' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>prose</a>.",
      link: "https://unocss.dev/presets/typography",
      body: `<article class="prose-pink lg:text-xl">
  <h1>Garlic bread with cheese: What the science tells us</h1>
  <p>
    For years parents have espoused the health benefits of eating garlic bread with cheese to their
    children, with the food earning such an iconic status in our culture that kids will often dress
    up as warm, cheesy loaf for Halloween.
  </p>
  <p>
    But a recent study shows that the celebrated appetizer may be linked to a series of rabies cases
    springing up around the country.
  </p>
</article>`
    }, {
      title: "Web Fonts preset",
      prose: true,
      description: "Any font available on <a href='https://fonts.google.com' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>Google Fonts</a>, can be used.",
      link: "https://unocss.dev/presets/web-fonts",
      body: `<p class="font-['Piazzolla']">The quick brown fox jumps over the lazy dog</p>
<p class="font-['Montserrat']">The quick brown fox jumps over the lazy dog</p>
<p class="font-['Marck_Script']">The quick brown fox jumps over the lazy dog</p>
<p class="font-['Open_Sans']">The quick brown fox jumps over the lazy dog</p>
<p class="font-['Roboto']">The quick brown fox jumps over the lazy dog</p>
<p class="font-['IBM_Plex_Serif']">The quick brown fox jumps over the lazy dog</p>
<p class="font-['Merriweather']">The quick brown fox jumps over the lazy dog</p>`
    }],
  },
  ru: {
    title4: "Перед использованием добавьте наименование шрифта через диалоговое окно добавления шрифтов",
    result: "Результат",
    title32: "Что почитать про атомарный CSS?",
    title1: "Предотвращение FOUC",
    title2: "Сброс стилей браузера",
    desc1: "Используйте атрибут un-cloak для предотвращения мерцания нестилизованного содержимого.",
    desc2: "Стили браузера сброшены по схеме \"Tailwind compat\".",
    details: "Подробности",
    subtitle21: "Интерактивная документация UnoCSS",
    subtitle22: "Документация Tailwind CSS",
    href22: "https://tailwindcss.ru/docs/utility-first",
    presets: [{
      title: "Wind4 preset",
      prose: false,
      description: "<a href='https://tailwindcss.ru' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>Tailwind CSS</a> доступна для использования без каких-либо дополнительных настроек.",
      link: "https://unocss.dev/presets/wind4",
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
      description: "Любая иконка из проекта <a href='https://icon-sets.iconify.design' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>Iconify</a> доступна по первому требованию.",
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
      description: "Красивые типографские настройки <a href='https://tailwindcss.ru/docs/typography-plugin' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>prose</a> для HTML.",
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
      description: "Любой шрифт, доступный на <a href='https://fonts.google.com' target='_blank' rel='noopener noreferrer' class='text-color-blue-500 hover:underline'>Google Fonts</a>, может быть использован.",
      link: "https://unocss.dev/presets/web-fonts",
      body: `<p class="font-['Piazzolla']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Montserrat']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Marck_Script']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Open_Sans']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Roboto']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['IBM_Plex_Serif']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>
<p class="font-['Merriweather']">Съешь ещё этих мягких французских булок, да выпей же чаю</p>`
    }],
  }
},
  { t } = useI18n({ messages });
</script>
