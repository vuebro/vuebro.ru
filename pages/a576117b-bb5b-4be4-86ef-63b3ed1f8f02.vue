<template>
<div class="container mx-auto my-24" un-cloak>
    <div class="text-center">
        <h2>{{ the.title }}</h2>
        <el-text size="large">{{ the.description }}</el-text>
    </div>
</div>
<div class="grid grid-cols-1 2xl:grid-cols-2 gap-4 mx-4" un-cloak>
    <div class="text-center flex flex-col 2xl:row-start-auto" v-for="({title, description, icon},index) in first"
        :class="{ 'row-start-5': index }">
        <icon class="size-24 mx-auto" :icon="icon"></icon>
        <h2>{{ title }}</h2>
        <el-text size="large">{{ description }}</el-text>
    </div>
    <el-alert :title="title" type="info" :description="description" show-icon :closable="false"
        v-for="({title, description},index) in second" class="2xl:row-start-auto"
        :class="{ 'row-start-6': index }"></el-alert>
    <el-tabs class="not-prose 2xl:row-start-auto" v-for="({html,js,css},index) in third"
        :class="{ 'row-start-7': index }">
        <el-tab-pane label="Template">
            <highlightjs language="html" :code="html"></highlightjs>
        </el-tab-pane>
        <el-tab-pane label="Script" v-if="js">
            <highlightjs language="js" :code="js"></highlightjs>
        </el-tab-pane>
        <el-tab-pane label="Style" v-if="css">
            <highlightjs language="css" :code="css"></highlightjs>
        </el-tab-pane>
        <el-tab-pane label="Результат" v-if="index">
            <div class="mx-6 mb-6 p-6 max-w-sm bg-white rounded-xl shadow-lg flex items-center space-x-4">
                <div class="shrink-0">
                    <icon icon="token-branded:chat" class="size-12"></icon>
                </div>
                <div>
                    <div class="text-xl font-medium text-black">ChitChat</div>
                    <p class="text-slate-500">У вас новое сообщение!</p>
                </div>
            </div>
        </el-tab-pane>
        <el-tab-pane label="Результат" v-else>
            <form @submit.prevent="addTodo">
                <el-input v-model="newTodo" required placeholder="new todo"><template #append><el-button
                            native-type="submit">Добавить задачу</el-button></template></el-input>
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
                {{ hideCompleted ? 'Показать все' : 'Скрыть выполненные' }}
            </el-button>
        </el-tab-pane>
    </el-tabs>
    <el-alert :title="title" type="success" :closable="false" show-icon v-for="({title, links},index) in fourth"
        :class="{ 'row-start-8': index }" class="2xl:row-start-auto">
        <ul>
            <li v-for="{subtitle, href} in links"><el-link :href="href" target="_blank">{{ subtitle }}</el-link></li>
        </ul>
    </el-alert>
</div>
</template>

<script setup>
import { ref, computed, inject } from "vue";
const props = defineProps(["id"]);
const pages = inject("pages");
const the = pages[props.id];

const first = [{
    icon: "logos:vue",
    title: "Vue.S3 полностью поддерживает однофайловые компоненты Vue (SFC)",
    description: "Vue (произносится /vjuː/, примерно как view) — JavaScript фреймворк для создания пользовательских интерфейсов. Он создан на стандартах HTML, CSS и JavaScript и предоставляет декларативную и компонентную модель программирования, которая помогает эффективно разрабатывать пользовательские интерфейсы любой сложности."
}, {
    icon: "logos:unocss",
    title: "UnoCSS работает в Vue.S3 \"из коробки\" в runtime режиме",
    description: "UnoCSS — мгновенный (instant) атомарный CSS‑движок с максимальной производительностью и гибкостью."
}];

const second = [{
    title: "Пример использования Vue.js",
    description: "Ниже приведен пример из интерактивного учебника по Vue.js. Для просмотра результата выполнения кликните на закладку \"Результат\"."
}, {
    title: "Пример использования UnoCSS",
    description: "Ниже приведен пример из документации по Tailwind CSS. Для просмотра результата выполнения кликните на закладку \"Результат\"."
}];


const third = [{
    html: `<form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="new todo">
    <button>Добавить задачу</button>
</form>
<ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
</ul>
<button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Показать все' : 'Скрыть выполненные' }}
</button>`,
    js: `import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Изучить HTML', done: true },
  { id: id++, text: 'Изучить JavaScript', done: true },
  { id: id++, text: 'Изучить Vue', done: false }
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
}`,
    css: `.done {
  text-decoration: line-through;
}`
},
{
    html: `<div class="mx-6 mb-6 p-6 max-w-sm bg-white rounded-xl shadow-lg flex items-center space-x-4">
    <div class="shrink-0">
        <icon icon="token-branded:chat" class="size-12"></icon>
    </div>
    <div>
        <div class="text-xl font-medium text-black">ChitChat</div>
        <p class="text-slate-500">У вас новое сообщение!</p>
    </div>
</div>`
}];

const fourth = [{
    title: "Что почитать про Vue.js?",
    links: [{
        subtitle: "Интерактивный учебник",
        href: "https://ru.vuejs.org/tutorial"
    }, {
        subtitle: "Руководство",
        href: "https://ru.vuejs.org/guide/introduction.html"
    }]
}, {
    title: "Что почитать про атомарный CSS?",
    links: [{
        subtitle: "Интерактивная документация UnoCSS",
        href: "https://unocss.dev/interactive"
    }, {
        subtitle: "Документация Tailwind CSS",
        href: "https://tailwindcss.ru/docs/utility-first"
    }]
}];

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([{
    id: id++,
    text: 'Изучить HTML',
    done: true
},
{
    id: id++,
    text: 'Изучить JavaScript',
    done: true
},
{
    id: id++,
    text: 'Изучить Vue',
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
