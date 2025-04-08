<template>
    <div class="container mx-auto px-4" un-cloak>
        <div class="flex flex-col text-center not-prose mb-24">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <div class="grid grid-cols-1 2xl:grid-cols-2 gap-4 mx-4">
            <div class="text-center flex flex-col 2xl:row-start-auto"
                v-for="({ title, description, icon }, index) in first" :class="{ 'row-start-5': index }">
                <icon class="size-24 mx-auto" :icon="icon"></icon>
                <h2>{{ title }}</h2>
                <el-text size="large">{{ description }}</el-text>
            </div>
            <el-alert :title="title" type="info" :description="description" show-icon :closable="false"
                v-for="({ title, description }, index) in second" class="2xl:row-start-auto"
                :class="{ 'row-start-6': index }"></el-alert>
            <el-tabs class="not-prose 2xl:row-start-auto" v-for="({ html }, index) in third"
                :class="{ 'row-start-7': index }">
                <el-tab-pane label="Template">
                    <highlightjs language="html" :code="html"></highlightjs>
                </el-tab-pane>
                <el-tab-pane :label="t('result')" v-if="index">
                    <div class="my-6 p-6 max-w-sm mx-auto bg-white rounded-xl shadow-lg flex items-center gap-x-4">
                        <div class="shrink-0">
                            <icon icon="token-branded:chat" class="size-12"></icon>
                        </div>
                        <div>
                            <div class="text-xl font-medium text-black">ChitChat</div>
                            <p class="text-slate-500">{{ t("message") }}</p>
                        </div>
                    </div>
                </el-tab-pane>
                <el-tab-pane :label="t('result')" v-else>
                    <form @submit.prevent="addTodo">
                        <el-input v-model="newTodo" required placeholder="new todo"><template #append><el-button
                                    native-type="submit">{{ t("button") }}</el-button></template></el-input>
                    </form>
                    <ul class="my-2">
                        <li v-for="todo in filteredTodos" :key="todo.id">
                            <el-input readonly :class="{ done: todo.done }" v-model="todo.text">
                                <template #prepend><el-checkbox v-model="todo.done"></el-checkbox></template>
                                <template #append><el-button @click="removeTodo(todo)">X</el-button></template>
                            </el-input>
                        </li>
                    </ul>
                    <el-button @click="hideCompleted = !hideCompleted">
                        {{ hideCompleted ? t("show") : t("hide") }}
                    </el-button>
                </el-tab-pane>
            </el-tabs>
            <el-alert :title="title" type="success" :closable="false" show-icon
                v-for="({ title, links }, index) in fourth" :class="{ 'row-start-8': index }"
                class="2xl:row-start-auto">
                <ul>
                    <li v-for="{ subtitle, href } in links"><el-link :href="href" target="_blank">{{ subtitle
                            }}</el-link>
                    </li>
                </ul>
            </el-alert>
        </div>
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

<script setup>
import { useI18n } from "vue-i18n";
import { ref, computed, inject, reactive } from "vue";
import { ArrowLeft, ArrowRight } from "@element-plus/icons-vue";

const props = defineProps(["id"]);
const pages = inject("pages");
const the = pages[props.id];
const { t } = useI18n({
    messages: {
        en: {
            title11: "vueS3 fully supports Vue Single File Components (SFC)",
            description11: "Vue (pronounced /vjuː/, like view) is a JavaScript framework for building user interfaces. It builds on top of standard HTML, CSS, and JavaScript and provides a declarative, component-based programming model that helps you efficiently develop user interfaces of any complexity.",
            title12: "UnoCSS is already integrated into vueS3 and operates in runtime mode",
            description12: "UnoCSS - the instant atomic CSS engine with maximum performance and flexibility.",
            title21: "Example of Using Vue.js",
            description21: "Below is an example from the interactive Vue.js tutorial. To view the execution result, click on the \"Result\" tab.",
            title22: "Example of Using UnoCSS",
            description22: "Below is an example from the Tailwind CSS documentation. To view the execution result, click on the \"Result\" tab.",
            title31: "What to Read About Vue.js?",
            title32: "What to Read About Atomic CSS?",
            learn: "Learn",
            button: "Add Todo",
            show: "Show all",
            hide: "Hide completed",
            result: "Result",
            message: "You have a new message!",
            subtitle11: "Tutorial",
            href11: "https://vuejs.org/tutorial",
            subtitle12: "Guide",
            href12: "https://vuejs.org/guide/introduction.html",
            subtitle21: "UnoCSS Interactive Docs",
            subtitle22: "Tailwind CSS Documentation",
            href22: "https://v3.tailwindcss.com/docs/utility-first",
        },
        ru: {
            title11: "vueS3 полностью поддерживает однофайловые компоненты Vue (SFC)",
            description11: "Vue (произносится /vjuː/, примерно как view) — JavaScript фреймворк для создания пользовательских интерфейсов. Он создан на стандартах HTML, CSS и JavaScript и предоставляет декларативную и компонентную модель программирования, которая помогает эффективно разрабатывать пользовательские интерфейсы любой сложности.",
            title12: "UnoCSS уже подключен в vueS3 и работает в рантайм режиме",
            description12: "UnoCSS — мгновенный (instant) атомарный CSS‑движок с максимальной производительностью и гибкостью.",
            title21: "Пример использования Vue.js",
            description21: "Ниже приведен пример из интерактивного учебника по Vue.js. Для просмотра результата выполнения кликните на закладку \"Результат\".",
            title22: "Пример использования UnoCSS",
            description22: "Ниже приведен пример из документации по Tailwind CSS. Для просмотра результата выполнения кликните на закладку \"Результат\".",
            title31: "Что почитать про Vue.js?",
            title32: "Что почитать про атомарный CSS?",
            learn: "Изучить",
            button: "Добавить задачу",
            show: "Показать все",
            hide: "Скрыть выполненные",
            result: "Результат",
            message: "У вас новое сообщение!",
            subtitle11: "Интерактивный учебник",
            href11: "https://ru.vuejs.org/tutorial",
            subtitle12: "Руководство",
            href12: "https://ru.vuejs.org/guide/introduction.html",
            subtitle21: "Интерактивная документация UnoCSS",
            subtitle22: "Документация Tailwind CSS",
            href22: "https://tailwindcss.ru/docs/utility-first",
        }
    }
});
const first = reactive([{
    icon: "logos:vue",
    title: t("title11"),
    description: t("description11")
}, {
    icon: "logos:unocss",
    title: t("title12"),
    description: t("description12")
}]);

const second = reactive([{
    title: t("title21"),
    description: t("description21")
}, {
    title: t("title22"),
    description: t("description22")
}]);


const third = reactive([{
    html: `<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: '${t("learn")} HTML', done: true },
  { id: id++, text: '${t("learn")} JavaScript', done: true },
  { id: id++, text: '${t("learn")} Vue', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
<\/script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="new todo">
    <button>${t("learn")}</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? '${t("show")}' : '${t("hide")}' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>`
},
{
    html: `<div class="my-6 p-6 max-w-sm mx-auto bg-white rounded-xl shadow-lg flex items-center gap-x-4">
    <div class="shrink-0">
        <icon icon="token-branded:chat" class="size-12"></icon>
    </div>
    <div>
        <div class="text-xl font-medium text-black">ChitChat</div>
        <p class="text-slate-500">${t("message")}</p>
    </div>
</div>`
}]);

const fourth = reactive([{
    title: t("title31"),
    links: [{
        subtitle: t("subtitle11"),
        href: t("href11")
    }, {
        subtitle: t("subtitle12"),
        href: t("href12")
    }]
}, {
    title: t("title32"),
    links: [{
        subtitle: t("subtitle21"),
        href: "https://unocss.dev/interactive"
    }, {
        subtitle: t("subtitle22"),
        href: t("href22")
    }]
}]);

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([{
    id: id++,
    text: `${t("learn")} HTML`,
    done: true
},
{
    id: id++,
    text: `${t("learn")} JavaScript`,
    done: true
},
{
    id: id++,
    text: `${t("learn")} Vue`,
    done: false
}
])

const filteredTodos = computed(() => {
    return hideCompleted.value ?
        todos.value.filter((t) => !t.done) :
        todos.value
})

function addTodo() {
    todos.value.push({
        id: id++,
        text: newTodo.value,
        done: false
    })
    newTodo.value = ''
}

function removeTodo(todo) {
    todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
