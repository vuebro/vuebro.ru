<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-24">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <h3>{{ t("h_1") }}</h3>
        <p class="text-justify">{{ t("p_1") }}: <router-link :to="`/${t('link_1')}/`">{{ t("link_1") }}</router-link>.
        </p>
        <p class="text-justify">{{ t("p_2_1") }} <a :href="t('link_2')" target="_blank" rel="noopener noreferrer">Vue
                Router</a>, {{ t("p_2_2") }}:
        </p>
        <highlightjs :code="t('code')" class="not-prose"></highlightjs>
        <p class="text-justify">{{ t("p_3") }}</p>
        <ul>
            <li>{{ t("li_1") }}</li>
            <li>{{ t("li_2") }}</li>
        </ul>
        <p class="text-justify">{{ t("p_4") }}: <router-link :to="`/${t('link_4')}/`">{{ t("link_4") }}</router-link>.
        </p>
        <h3>{{ t("h_2") }}</h3>
        <p class="text-justify">{{ t("p_5") }}</p>
        <highlightjs class="not-prose" language="js" :code="t('inj')"></highlightjs>
        <p class="text-justify">{{ t("p_6") }}: <router-link :to="`/${t('link_5')}/`">{{ t("link_5") }}</router-link>.
        </p>
    </div>
</template>

<script setup>
import { inject } from "vue";
import { useI18n } from "vue-i18n";
const { id } = defineProps(["id"]),
    pages = inject("pages"),
    the = pages[id];
const { t } = useI18n({
    messages: {
        en: {
            h_1: "Category Tree",
            p_1: 'Pages in the veuS3 web editor are organized in a tree structure, which can be managed directly in the editor. You can create, delete, rename, and modify the semantics and content of pages. The only immutable part of this structure is the root of the tree, the "root page." This page is present in every site created with vueS3 and cannot be deleted. It plays a key role in building the site template and navigation. Additionally, it is a good idea to connect third-party modules and frameworks to the root page if they are used across most pages of your site. For more details, see',
            link_1: "documentation/modules",
            p_2_1: "For site navigation, vueS3 uses",
            link_2: "https://router.vuejs.org",
            p_2_2: "which manages which page of the site is displayed. To ensure the current page is rendered, you need to add the <router-view></router-view> tag to the root page template",
            p_3: "As a result, we get the root page, where the category tree is mounted at a point defined by you. On most websites, the following elements are also commonly used:",
            li_1: "Site Header : The title or header of the site.",
            li_2: "Site Footer : The footer of the site.",
            p_4: "Additionally, navigation elements such as menus and various bars are often used. These elements are either always visible on the site or temporarily hidden, ready to be displayed when needed. It is logical to place these elements on the root page. A simple example of how this is implemented can be seen at the following link",
            link_4: "documentation/start",
            h_2: "Semantic Objects of the Selected and Current Pages",
            p_5: "Of particular note is that on the root page, alongside the semantic object of the current page, the semantic object of the selected page is also in demand:",
            p_6: "It is indispensable in cases where you need to display information about the selected page, for example, to highlight the selected page in your menu. For more details",
            link_5: "documentation/semantics",
            code: `...
<!-- The point where the category tree is mounted -->
<router-view></router-view>
...`,
            inj: `/** Import computed and inject */
import {'{'} computed, inject {'}'} from "vue";
/** Import the composable for the selected route */
import {'{'} useRoute {'}'} from "vue-router";
/** Get the ID of the current page */
const {'{'} id {'}'} = defineProps(["id"]);
/** Get the object of the selected route */
const route = useRoute(),
/** Inject the array of semantic objects for the site's pages */
const pages = inject("pages");
/**  Get the semantic object of the current page */
const the = pages[id];
/** Compute the semantic object of the selected page */
const that = computed(() => pages[route.name]);`,
        },
        ru: {
            h_1: "Дерево рубрик",
            p_1: 'Страницы в веб-редакторе veuS3 организованы в виде дерева, которым можно управлять напрямую в редакторе. Можно создавать страницы, удалять, переименовывать, изменять их семантику и наполнение. Неизменным остается лишь корень дерева, "корневая страница". Она присутствует в любом сайте, сделанном на vueS3 и её нельзя удалить. Эта страница имеет ключевую роль в построении шаблона сайта и навигации по сайту. Также, хорошей идеей является подключение сторонних модулей и фреймворков именно к корневой странице, если таковые используются на большинстве страниц вашего сайта, подробности',
            link_1: "документация/модули",
            p_2_1: "Для навигации по сайту в veuS3 используется",
            link_2: "https://vue-router-ru.netlify.app",
            p_2_2: "именно он управляет тем, какая страница сайта отображается. Таким образом, чтобы обеспечить отображение текущей страницы, надо на корневую страницу, в шаблон добавить таг <router-view ></router-view >",
            p_3: "В итоге, мы получаем корневую страницу, где, в точку определенную вами, монтируется дерево рубрик. На большинстве сайтов используются также следующие элементы:",
            li_1: "Заголовок (хидер) сайта",
            li_2: "Подвал (футер) сайта",
            p_4: "Кроме того, зачастую используются элементы навигации, типа меню сайта и различных баров. Все эти элементы постоянно отображаются на сайте либо временно находятся в скрытом состоянии, чтобы быть отображенными по первому требованию. Разумно их размещать именно на корневой странице. Простой пример, как это реализовано, можно увидеть по ссылке",
            link_4: "документация/старт",
            h_2: "Семантические объекты выбранной и данной страниц",
            p_5: "Особенно стоит отметить, что на корневой странице, наряду с семантическим объектом данной страницы, востребован семантический объект выбранной страницы:",
            p_6: "Он незаменим в случаях, когда нужно отобразить информацию о выбранной странице, например, выделить выбранную страницу в вашем меню. Подробности",
            link_5: "документация/семантика",
            code: `...
<!-- Точка, куда монтируется дерево рубрик -->
<router-view></router-view>
...`,
            inj: `/** Импортируем вычислитель и инжектор */
import {'{'} computed, inject {'}'} from "vue";
/** Импортируем композабл выбранного роута */
import {'{'} useRoute {'}'} from "vue-router";
/** Получаем id данной страницы */
const {'{'} id {'}'} = defineProps(["id"]);
/** Получаем объект выбранного роута */
const route = useRoute(),
/** Инжектируем массив семантических объектов страниц сайта */
const pages = inject("pages");
/** Получаем семантический объект данной станицы */
const the = pages[id];
/** Вычисляем семантический объект выбранной страницы */
const that = computed(() => pages[route.name]);`,
        }
    }
});
</script>
