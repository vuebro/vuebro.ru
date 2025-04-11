<template>
    <el-carousel type="card" height="auto" indicator-position="outside" un-cloak>
        <el-carousel-item v-for="i in 6" class="!h-fit"><img :src="`images/screenshots/${i}.png`" decoding="async"></el-carousel-item>
    </el-carousel>
</template>