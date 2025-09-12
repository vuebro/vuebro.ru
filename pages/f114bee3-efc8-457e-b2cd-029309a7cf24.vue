<template>
    <div class="container mx-auto px-4">
        <div class="flex flex-col text-center not-prose mb-24">
            <icon :icon="the.icon" class="size-20 mx-auto"></icon>
            <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
            <el-text size="large">{{ the.description }}</el-text>
        </div>
        <h3>{{ t(0) }}</h3>
        <p>{{ t(10) }}</p>
        <h3>{{ t(20) }}</h3>
        <ol>
            <li><a href="https://console.mistral.ai/api-keys" target="_blank" rel="noopener noreferrer">{{ t(30) }}</a>
            </li>
            <li>
                <div class="grid grid-cols-1 gap-6 lg:grid-cols-8">
                    <div class="col-span-1 lg:col-span-5 text-justify">{{ t(40) }}
                        <el-alert :title="t(50)" type="warning" :closable="false" :description="t(60)" show-icon=""
                            class="!mt-4"></el-alert>
                    </div>
                    <div class="col-span-1 lg:col-span-3 not-prose"><el-image src="/images/screenshots/7.png"
                            :preview-src-list="['/images/screenshots/7.png']" class="w-full h-auto">
                        </el-image></div>
                </div>
            </li>
            <li>
                <div class="grid grid-cols-1 gap-6 lg:grid-cols-8">
                    <div class="col-span-1 lg:col-span-5 text-justify">
                        <i18n-t keypath="70">
                            <el-tag>Ctrl+Shift+Space</el-tag>
                            <el-tag>Complete Code</el-tag>
                        </i18n-t>
                    </div>
                    <div class="col-span-1 lg:col-span-3 not-prose"><el-image src="/images/screenshots/8.png"
                            :preview-src-list="['/images/screenshots/8.png']" class="w-full h-auto">
                        </el-image></div>
                </div>
            </li>
        </ol>
        <p>{{ t(80) }}</p>
        <div class="not-prose flex mt-48">
            <el-button-group class="mx-auto" size="large">
                <el-button class="my-1" type="primary" :icon="ArrowLeft" :to="the.$prev.to" v-if="the.$prev"
                    tag="router-link">{{
                        the.$prev.header }}</el-button>
                <el-button class="my-1" type="primary" v-if="the.$next" :to="the.$next.to" tag="router-link">{{
                    the.$next.header
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

const { pid } = defineProps(["pid"]),
    pages = inject("pages"),
    the = pages[pid],
    { t } = useI18n({
        messages: {
            ru: {
                0: "Поддержка нейросетей",
                10: "Современное программирование стремительно меняется. Новые подходы, методы, инструменты и, конечно же, нейросети. К ним можно относится по разному, но без сомнения при должной сноровке нейросети помогают программисту избавиться от рутинных задач. А значит, у разработчика остается больше времени и сил для самых смелых реализации идей и замыслов. К VueBro тоже можно подключить умного помошника -&nbsp;Codestral от Mistral.",
                20: "Порядок подключения",
                30: "Получить Mistral API Key",
                40: "Вставить ключ в настройки VueBro",
                50: "Внимание!",
                60: "Используйте ключ только на безопасном компьютере. Пожалуйста, во избежании кражи ключа не используйте его на компьютерах с общим доступом.",
                70: "В режиме редактирования исходного кода нажмите {0} или выберите мышкой элемент контекстного меню {1}.",
                80: "Нейросеть работает в контексте текущей страницы и неплохо показывает себя в задачах автодополнения кода. А если написать для нее комментарии в теле кода с подробным описанием задачи, она способна довольно качественно решить её. Все зависит от того, насколько подробно и четко поставить задачу для искусственного интеллекта."
            },
            en: {
                0: "Neural network support",
                10: "Modern programming is changing rapidly. New approaches, methods, tools, and, of course, neural networks. You can relate to them in different ways, but without a doubt, with proper skill, neural networks help the programmer to get rid of routine tasks. This means that the developer has more time and energy for the boldest implementation of ideas and concepts. You can also connect a smart assistant to VueBro - Codestral from Mistral.",
                20: "Connection order",
                30: "Get Mistral API Key",
                40: "Insert the key into VueBro settings",
                50: "Attention!",
                60: "Use the key only on a secure computer. Please, to avoid key theft, do not use it on computers with shared access.",
                70: "In the source code editing mode, press {0} or select the context menu item {1} with the mouse.",
                80: "The neural network operates within the context of the current page and performs well in code autocompletion tasks. If you provide detailed comments in the code describing the task, it can solve the problem quite effectively. The quality of the result depends on how clearly and thoroughly the task is defined for the artificial intelligence."
            }
        }
    });

</script>
