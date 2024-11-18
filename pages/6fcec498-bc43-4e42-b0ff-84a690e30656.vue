<template>
<v-card class="mx-auto" max-width="344" subtitle="Same looks, no anchor" title="Hover and click me" link></v-card>
</template>

<script setup>
import "./node_modules/vuetify/dist/vuetify.min.css";
import { createVuetify, components, directives } from "./node_modules/vuetify/dist/vuetify.esm.js";

const vuetify = createVuetify({
    components,
    directives,
});

window.app.use(vuetify);
</script>


