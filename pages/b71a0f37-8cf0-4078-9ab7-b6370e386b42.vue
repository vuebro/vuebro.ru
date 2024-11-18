<template>
<div class="container mx-auto px-4">
  <div class="flex flex-col text-center not-prose">
    <icon :icon="the.icon" class="size-20 mx-auto"></icon>
    <h2 class="text-4xl my-5 font-['Caveat']">{{ the.title }}</h2>
    <el-text size="large">{{ the.description }}</el-text>
  </div>
    <h3>Структура файлов по-умолчанию</h3>
    <p>Такой набор папок и файлов вы увидите в корзине после запуска VueS3:</p>
    <ul class="not-prose pl-5 list-none list-inside mb-12">
        <li><el-text tag="b"><el-icon>
                    <Folder />
                </el-icon> /</el-text><el-text> - корневая директория бакета</el-text>
            <ul class="list-none list-inside ml-4">
                <li><el-text tag="b"><el-icon>
                            <Folder />
                        </el-icon> .vite</el-text><el-text> - папка для хранения манифеста vite</el-text>
                    <ul class="list-none list-inside ml-8">
                        <li><el-text tag="b"><el-icon>
                                    <Document />
                                </el-icon> manifest.json</el-text><el-text> - файл манифеста, предназначенный для
                                синхронизации системных модулей</el-text></li>
                    </ul>
                </li>
                <li><el-text tag="b"><el-icon>
                            <Folder />
                        </el-icon> assets</el-text><el-text> - системные модули, обеспечивающие работоспособность
                        сайта</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Folder />
                        </el-icon> images</el-text><el-text> - загруженные изображения</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Folder />
                        </el-icon> pages</el-text><el-text> - sfc компоненты в формате json для каждой
                        страницы</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Document />
                        </el-icon> index.html</el-text><el-text> - загрузочный файл</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Document />
                        </el-icon> index.json</el-text><el-text> - иерархическая структура семантических атрибутов всех
                        страниц сайта</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Document />
                        </el-icon> index.importmap</el-text><el-text> - список импортируемых модулей</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Document />
                        </el-icon> robots.txt</el-text><el-text> - рекомендации для поисковиков</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Document />
                        </el-icon> sitemap.xml</el-text><el-text> - карта сайта для поисковиков</el-text></li>
                <li><el-text tag="b"><el-icon>
                            <Document />
                        </el-icon> favicon.ico</el-text><el-text> - фавиконка</el-text></li>
            </ul>
        </li>
    </ul>
    <el-alert title="Внимание!!!" type="error"
        description="VueS3 никогда не удаляет ни папки ни файлы. Так сделано из соображений безопасности." show-icon
        :closable="false" class="not-prose" />
    <h3>Динамическая структура папок</h3>
    <p>По мере создания рубрик в древовидной структуре VueS3, создаются папки соответствующие роутам.
        В созданные папки помещается файл index.html, идентичный тому, что находится в корне.
        Процесс создания папок и обновления файлов index.html полностью автоматический и предназначен для обеспечения
        SEO.</p>
</div>
</template>

<script setup>
import { Folder, Document } from "@element-plus/icons-vue";
import { inject } from "vue";
const { id } = defineProps(["id"]);
const pages = inject("pages");
const the = pages[id];

</script>


