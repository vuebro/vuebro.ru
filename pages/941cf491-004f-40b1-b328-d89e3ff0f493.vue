<template>
  <div class="container mx-auto px-4" un-cloak>
    <div class="flex flex-col text-center not-prose mb-24">
      <icon :icon="the.icon" class="size-20 mx-auto"></icon>
      <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
      <el-text size="large">{{ the.description }}</el-text>
    </div>
    <h3>{{ t("h3[0]") }}</h3>
    <p><span v-html="t('p[0]')"></span> <router-link :to="`/${t('routerlink[0]')}/`">{{ t("routerlink[0]")
        }}</router-link>.</p>
    <h3>{{ t("h3[1]") }}</h3>
    <p v-html="t('p[1]')"></p>
    <h3>Sitemap.xml</h3>
    <p v-html="t('p[2]')"></p>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit not-prose">
      <dt class="font-bold text-slate-700">loc:</dt>
      <dd class="text-slate-500">{{ t("dd[0]") }}</dd>
      <dt class="font-bold text-slate-700">changefreq:</dt>
      <dd class="text-slate-500">{{ t("dd[1]") }}</dd>
      <dt class="font-bold text-slate-700">priority:</dt>
      <dd class="text-slate-500">{{ t("dd[2]") }}</dd>
      <dt class="font-bold text-slate-700">lastmod:</dt>
      <dd class="text-slate-500">{{ t("dd[3]") }}</dd>
    </dl>
    <p><span v-html="t('p[3]')"></span> <router-link :to="`/${t('routerlink[0]')}/`">{{ t("routerlink[0]")
        }}</router-link>.</p>
    <h3>{{ t("h3[2]") }}</h3>
    <div class="my-10"><el-alert type="info" :closable="false" :title="t('title[0]')" effect="dark"><img
          :src="the.images[1].url"></el-alert></div>
    <h3>Robots.txt</h3>
    <p>{{ t("p[4]") }}</p>
    <div class="my-10"><el-alert type="info" :closable="false" :title="t('title[1]')" effect="dark"><img
          :src="the.images[2].url"></el-alert></div>
    <h3>Favicon.ico</h3>
    <p>{{ t("p[5]") }}</p>
    <div class="my-10"><el-alert type="info" :closable="false" :title="t('title[2]')" effect="dark"><img
          :src="the.images[3].url"></el-alert></div>
    <h3>Json-LD</h3>
    <p>{{ t("p[6]") }}</p>
    <div class="my-10"><el-alert type="info" :closable="false" :title="t('title[3]')" effect="dark"><img
          :src="the.images[4].url"></el-alert></div>
    <p><span v-html="t('p[7]')"></span> <router-link :to="`/${t('routerlink[0]')}/`">{{ t("routerlink[0]")
        }}</router-link>.</p>
    <h3>Open Graph</h3>
    <p>{{ t("p[8]") }}</p>
    <br>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit not-prose">
      <dt class="font-bold text-slate-700">type:</dt>
      <dd class="text-slate-500">{{ t("dd[4]") }}</dd>
      <dt class="font-bold text-slate-700">header:</dt>
      <dd class="text-slate-500">{{ t("dd[5]") }}</dd>
      <dt class="font-bold text-slate-700">description:</dt>
      <dd class="text-slate-500">{{ t("dd[6]") }}</dd>
      <dt class="font-bold text-slate-700">keywords:</dt>
      <dd class="text-slate-500">{{ t("dd[7]") }}</dd>
    </dl>
    <p>{{ t("p[9]") }}</p>
    <highlightjs class="not-prose" :code="code1"></highlightjs>
    <h3>{{ t("h3[3]") }}</h3>
    <div class="my-10"><el-alert type="info" :closable="false" :title="t('title[4]')" effect="dark"><img
          :src="the.images[5].url"></el-alert></div>
    <p>{{ t("p[10]") }}</p>
    <dl class="grid grid-cols-[repeat(2,auto)] gap-x-4 w-fit not-prose">
      <dt class="font-bold text-slate-700">images:</dt>
      <dd class="text-slate-500">{{ t("dd[8]") }}</dd>
    </dl>
    <p>{{ t("p[11]") }}</p>
    <highlightjs class="not-prose" :code="code2"></highlightjs>
    <p><span v-html="t('p[12]')"></span> <router-link :to="`/${t('routerlink[0]')}/`">{{ t("routerlink[0]")
        }}</router-link>.</p>
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
import { ArrowLeft, ArrowRight } from "@element-plus/icons-vue";
import { useI18n } from "vue-i18n";
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
<meta property="og:image:alt" content="image_alt_n" />`,
  { t } = useI18n({
    messages: {
      en: {
        h3: [
          "Semantic Core",
          "Page Generation",
          "Domain",
          "Images"
        ],
        p: [
          `Pages in VueBro are organized in a tree-like structure, and each page has an attached semantic object containing a set of attributes. Together, these form the **semantic core** of the website. 
The key attribute in each set is <b>name</b>, which stores the page title. These names are used to generate the paths leading to each page based on their position within the tree structure. The resulting paths are stored in the <b>path</b> attribute.
For more details on the full list of attributes, see the section:`,
          `In VueBro, special attention is given to search engine optimization. Flawless accessibility for search engines is ensured by generating a set of pages corresponding to the site’s routes. These pages are technically identical to the main page and serve exclusively to load the site's modules, differing only in the set of search meta tags specific to each individual page. As a result, even search engine crawlers that evaluate only static website content receive correct search semantics.
For modern search engine crawlers capable of analyzing dynamic websites, the system includes dynamic SEO data updates through the use of the <a href="https://unhead.unjs.io"
        target="_blank" rel="noopener noreferrer">unhead</a> library.`,
          `To provide information about the structure of pages, VueBro generates a <a href="https://www.sitemaps.org"
        target="_blank" rel="noopener noreferrer">sitemap.xml</a> file. This file is automatically created based on the site's page tree.  
On each page, you can specify additional attributes that will also be included in the sitemap.xml file for the corresponding pages.`,
          "Access to the attributes is available through the page's semantic object. For details, see the section:",
          "Robots.txt is a text file that contains site indexing parameters for the search engine robots. When crawling a site, the Yandex robot loads the robots.txt file. If the latest request to the file shows that a site page or section is prohibited, the robot won't index them.",
          "The file can be edited through the robots.txt dialog window.",
          "The website's icon changes dynamically depending on the icon selected for the page in the <b>icon</b> setting.",
          "To ensure that search engines correctly interpret the pages of your website, add structured data to them. With structured data, you can describe pages and classify their content in a format that search engines understand.",
          "The entered data is injected into the corresponding pages of the website and is also available through the `jsonld` attribute of the page's semantic object. For details, see the section:",
          "The following attributes are used to create SEO meta tags, which can be set for each page of the website:",
          "Based on the entered values, the following set of meta tags is generated for each page:",
          "All added images are saved in the attribute array:",
          "From the images attribute array, a set of meta tags is generated for the corresponding pages:",
          "Access to images is also available through the page's semantic object. For details, see the section:"
        ],
        routerlink: ["documentation/semantics"],
        dd: [
          "Alternative page URL.",
          "How frequently the page is likely to change. This value provides general information to search engines and may not correlate exactly to how often they crawl the page.",
          "The priority of this URL relative to other URLs on your site. Valid values range from 0.0 to 1.0. This value does not affect how your pages are compared to pages on other sites—it only lets the search engines know which pages you deem most important for the crawlers.",
          "The date of last modification of the page.",
          "Object type, for example, video.movie (movie). If there are multiple objects on the page, select one (the main object). Depending on the type, you can specify additional properties.",
          "Page title",
          "Page description",
          "Keywords for the page",
          "Array of objects {'{'}url, alt{'}'}, where: url — image URL, alt — image description"
        ],
        title: [
          "To generate the sitemap.xml file, you must specify the website's domain in the domain input dialog. If the domain is not specified, the sitemap.xml file will not be created.",
          "The file can be edited through the robots.txt dialog window",
          "For compatibility with outdated search engine crawlers, there is an option to upload a favicon.ico file through a dedicated dialog window.",
          "To enter and edit the data, go to the JSON-LD tab.",
          "To add images that illustrate the page, use the IMAGES tab."
        ],
      },
      ru: {
        h3: [
          "Семантическое ядро",
          "Генерация страниц",
          "Домен",
          "Картинки"
        ],
        p: [
          `Страницы в VueBro организованы в виде древовидной структуры, при этом к каждой из страниц прикреплен
      семантический объект с набором атрибутов, что в совокупности образует семантическое ядро сайта. Ключевой атрибут в
      каждом из наборов носит имя <b>name</b> и отвечает за хранение названий
      страниц, из которых формируются пути до любой из страниц сайта относительно нахождения страницы в древовидной
      структуре. Пути, в свою очередь, хранятся в атрибутах <b>path</b>. Подробнее о составе
      атрибутов см. в разделе`,
          `В VueBro особое внимание уделено поисковой оптимизации. Безукоризненная
      доступность для поисковых машин обеспечивается созданием набора
      страниц, соответствующих
      роутам сайта. Технически они идентичны главной странице сайта и служат исключительно загрузке программных
      модулей, отличаясь лишь набором поисковых мета тагов, соответствующих конкретной странице на сайте. В результате
      даже
      поисковые роботы, которые оценивают исключительно статическую выдачу сайта, получают корректную поисковую
      семантику.
      Для
      современных поисковых роботов, умеющих анализировать динамические сайты, в сайт встроено динамическое
      обновление данных для seo посредством задействования библиотеки <a href="https://unhead.unjs.io"
        target="_blank" rel="noopener noreferrer">unhead</a>.`,
          `Для передачи информации о составе страниц VueBro создает файл <a href="https://www.sitemaps.org/ru"
        target="_blank" rel="noopener noreferrer">sitemap.xml</a>. Файл формируется в автоматическом режиме на основе
      дерева
      страниц сайта. На каждой странице возможно указать дополнительные атрибуты, которые также будут добавлены в файл
      sitemap.xml для соответствующих страниц.`,
          "Доступ к атрибутам возможен через семантический объект страницы. Подробности см. в разделе",
          "Robots.txt — это текстовый файл, который содержит параметры индексирования сайта для роботов поисковых систем. В robots.txt можно ограничить индексирование роботами страниц сайта, что может снизить нагрузку на сайт и ускорить его работу.",
          "Иконка на сайте меняется динамически в зависимости от выбранной иконки для страницы в параметре <b>icon</b>.",
          "Чтобы поисковики правильно интерпретировали страницы вашего сайта, добавьте на них структурированные данные. С их помощью вы можете описывать страницы и классифицировать контент на них в формате, понятном поисковым машинам.",
          "Введенные данные инжектируются в соответствующие страницы сайта, а также доступны через атрибут jsonld семантического объекта страницы. Подробности см. в разделе",
          "Для создания SEO тагов используются следующие атрибуты, которые возможно задать для каждой страницы сайта:",
          "На основе введенных значений формируется следующий набор тагов для каждой страницы:",
          "Все добавленные картинки сохнаняются в массив атрибутов:",
          "Из массива атрибутов images формируется набор тагов для соответствующих страниц:",
          "Доступ к картинкам также возможен через семантический объект страницы. Подробности см. в разделе"
        ],
        routerlink: ["документация/семантика"],
        dd: [
          "Альтернативная ссылка на страницу.",
          "Вероятная частота изменения этой страницы. Это значение предоставляет общую информацию для поисковых систем и может не соответствовать точно частоте сканирования этой страницы.",
          "Приоритетность URL относительно других URL на Вашем сайте. Допустимый диапазон значений — от 0,0 до 1,0. Это значение не влияет на процедуру сравнения Ваших страниц со страницами на других сайтах — оно только позволяет указать поисковым системам, какие страницы, по Вашему мнению, более важны для сканеров.",
          "Дата последнего изменения страницы.",
          "Тип объекта, например, video.movie (фильм). Если у вас несколько объектов на странице, выберите один из них (главный). В зависимости от типа можно указать дополнительные свойства.",
          "Заголовок страницы",
          "Описание страницы",
          "Ключевые слова для страницы",
          "Массив объектов {'{'}url, alt{'}'}, где: url - адрес картинки, alt - описание картинки"
        ],
        title: [
          "Для генерации файла sitemap.xml необходимо указать домен сайта в диалоговом окне для ввода домена. Если домен не указан, файл sitemap.xml не создается.",
          "Отредактировать файл можно через диалоговое окно для robots.txt",
          "Для совместимости с устаревшими поисковыми роботами предусмотрена возможность загрузки файла favicon.ico через специальное диалоговое окно.",
          "Для ввода и редактирования данных перейдите в закладку JSON-LD.",
          "Для добавления изображений, которые используются для иллюстрации страницы используйте закладку IMAGES."
        ],
      },
    }
  });
</script>
