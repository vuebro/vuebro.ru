<template>
  <div class="container mx-auto">
    <div class="flex flex-col text-center not-prose mb-24">
      <icon :icon="the.icon" class="size-20 mx-auto"></icon>
      <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
      <el-text size="large">{{ the.description }}</el-text>
    </div>
    <h3>Семантическое ядро</h3><div>Страницы в vueS3 организованы в виде древовидной структуры. В этой структуре к каждой из страниц прикреплен семантический объект с набором атрибутов, что в совокупности образует семантическое ядро сайта. Ключевой атрибут в каждом из наборов носит имя name и отвечает за хранение н<span style="color: var(--un-prose-body);">азваний страниц, из которых формируются пути до любой из страниц сайта относительно нахождения страницы в древовидной структуре. Пути, в свою очередь, хранятся в атрибутах path.</span><span style="color: var(--un-prose-body);">&nbsp;</span><span style="color: var(--un-prose-body);">Подробнее о составе атрибутов см. в разделе</span><span style="color: var(--un-prose-body);">&nbsp;</span><router-link to="https://run.vues3.ru/%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F/%D1%81%D0%B5%D0%BC%D0%B0%D0%BD%D1%82%D0%B8%D0%BA%D0%B0/">документация/семантика</router-link><span style="color: var(--un-prose-body);">.</span></div><h3>Генерация страниц</h3>
    <div>В vueS3 особое внимание уделено поисковой оптимизации. Для обеспечения безукоризненной
      доступности для поисковых машин vueS3 создает набор
      страниц, соответствующих
      роутам сайта. Технически они идентичны главной странице сайта и служат исключительно загрузке программных
      модулей
      сайта с
      отличием лишь в наборе поисковых мета тагов, соответствующих конкретной странице на сайте. В результате даже
      поисковые роботы, которые оценивают только статическую выдачу сайта, получают корректную поисковую семантику.
      Для
      современных поисковых роботов, которые умеют анализировать динамические сайты, в сайт встроено динамическое обновление данных для seo посредством задействования библиотеки <a href="https://unhead.unjs.io" target="_blank">unhead</a>.
    </div>
    <h3>Sitemap</h3>
    <p>Для передачи информации о составе страниц vueS3 создает файл <a href="https://www.sitemaps.org/ru">sitemap.xml</a>. Файл формируется в автоматическом режиме на основе дерева
      страниц сайта. На каждой странице возможно указать дополнительные атрибуты, которые также будут добавлены в файл
      sitemap.xml для соответствующих страниц.</p>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
      <dt class="font-bold text-slate-700">loc:</dt>
      <dd class="text-slate-500">Альтернативная ссылка на страницу</dd>
      <dt class="font-bold text-slate-700">changefreq:</dt>
      <dd class="text-slate-500">Вероятная частота изменения этой страницы. Это значение предоставляет общую информацию
        для поисковых систем и может не соответствовать точно частоте сканирования этой страницы.</dd>
      <dt class="font-bold text-slate-700">priority:</dt>
      <dd class="text-slate-500">Приоритетность URL относительно других URL на Вашем сайте. Допустимый диапазон значений
        — от 0,0 до 1,0. Это значение не влияет на процедуру сравнения Ваших страниц со страницами на других сайтах —
        оно только позволяет указать поисковым системам, какие страницы, по Вашему мнению, более важны для сканеров.
      </dd>
      <dt class="font-bold text-slate-700">lastmod:</dt>
      <dd class="text-slate-500">Дата последнего изменения</dd>
    </dl>
    <p>Доступ к атрибутам возможен через семантический объект страницы. Подробности см. в разделе <router-link to="/документация/семантика/">документация/семантика</router-link>.</p>
    <p></p>
    <h3>Домен</h3>
    <div>Для генерации файла sitemap.xml необходимо указать домен сайта в диалоговом окне для ввода домена. Если домен
      не указан, файл sitemap.xml не создается.</div>
    <h3>Robots.txt</h3>
    <div>Robots.txt — это текстовый файл, который содержит параметры индексирования сайта для роботов поисковых систем.
      В robots.txt можно ограничить индексирование роботами страниц сайта, что может снизить нагрузку на сайт и ускорить
      его работу. Отредактировать файл можно через диалоговое окно для robots.txt</div>
    <h3>Favicon.ico</h3>
    <p>Иконка на сайте меняется динамически в зависимости от выбранной иконки для страницы в
      параметре <b>icon</b>. Для совместимости с устаревшими поисковыми роботами предусмотрена возможность
      загрузки файла favicon.ico через специальное диалоговое окно.</p>
    <h3>Json-LD</h3>
    <p>Чтобы поисковики правильно интерпретировали страницы вашего сайта, добавьте на них структурированные данные. С
      их помощью вы можете описывать страницы и классифицировать контент на них в формате, понятном поисковым машинам.
      Для ввода и редактирования данных перейдите в закладку JSON-LD. Введенные данные инжектируются в
      соответствующие страницы сайта, а также доступны через атрибут jsonld семантического объекта
      страницы.&nbsp;Подробности см. в разделе&nbsp;<router-link to="https://run.vues3.ru/%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0%D1%86%D0%B8%D1%8F/%D1%81%D0%B5%D0%BC%D0%B0%D0%BD%D1%82%D0%B8%D0%BA%D0%B0/">документация/семантика</router-link>.&nbsp;
    </p>
    <h3>Open Graph</h3>
    <p>Для создания SEO тагов используются следующие атрибуты, которые возможно задать для каждой страницы сайта:</p>
    <br>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
      <dt class="font-bold text-slate-700">type:</dt>
      <dd class="text-slate-500">Тип объекта, например, video.movie (фильм). Если у вас несколько объектов на странице,
        выберите один из них (главный). В зависимости от типа можно указать дополнительные свойства.</dd>
      <dt class="font-bold text-slate-700">header:</dt>
      <dd class="text-slate-500">Заголовок страницы</dd>
      <dt class="font-bold text-slate-700">description:</dt>
      <dd class="text-slate-500">Описание страницы</dd>
      <dt class="font-bold text-slate-700">keywords:</dt>
      <dd class="text-slate-500">Ключевые слова для страницы</dd>
    </dl>
    <p>На основе введенных значений формируется следующий набор тагов для каждой страницы:</p>
    <highlightjs class="not-prose" :code="code1"></highlightjs>
    <h3>Картинки</h3>
    <p>Для добавления изображений, которые используются для иллюстрации страницы используйте закладку IMAGES. Все добавленные картинки сохнаняются в массив атрибутов:</p>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit">
      <dt class="font-bold text-slate-700">images:</dt>
      <dd class="text-slate-500">Массив объектов {url, alt}, где: url - адрес картинки, alt - описание картинки</dd>
    </dl>
    <p>Из массива атрибутов images формируется набор тагов для соответствующих страниц:</p>
    <highlightjs class="not-prose" :code="code2"></highlightjs>
    <p>Доступ к картинкам также возможен через семантический объект страницы. Подробности см. в разделе <router-link to="/документация/семантика/">документация/семантика</router-link>.</p>
    <div class="not-prose flex mt-48">
      <el-button-group class="mx-auto">
        <el-button type="primary" :icon="ArrowLeft" :to="the.$prev.to" v-if="the.$prev" tag="router-link">{{
          the.$prev.header }}</el-button>
        <el-button type="primary" v-if="the.$next" :to="the.$next.to" tag="router-link">{{ the.$next.header
        }}<el-icon class="el-icon--right">
            <arrowright></arrowright>
          </el-icon></el-button>
      </el-button-group>
    </div>
  </div>
</template>

<script setup vapor>
import { ArrowLeft, ArrowRight } from "@element-plus/icons-vue";
import { inject } from "vue";

const { id } = defineProps(["id"]),
  pages = inject("pages"),
  the = pages[id],
  code1 = `<title>title</title>
<meta name="description" content="description" />
<meta name="keywords" content="" />
<meta property="og:title" content="title" />
<meta property="og:description" content="description" />
<meta property="og:type" content="type" />
<meta property="og:url" content="url" />`,
  code2 = `<meta property="og:image" content="image_1" />
<meta property="og:image:alt" content="image_alt_1" />
...
<meta property="og:image" content="image_n" />
<meta property="og:image:alt" content="image_alt_n" />`;
</script>
