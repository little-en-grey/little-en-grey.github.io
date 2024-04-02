<template>
    <v-app>
        <v-app-bar fixed app>
            <v-toolbar-title>{{ pageTitle }}</v-toolbar-title>
        </v-app-bar>
        <v-main>
            <slot />
        </v-main>
        <v-footer app>
            <span>&copy; {{ new Date().getFullYear() }} {{ pageTitle }}</span>
        </v-footer>
    </v-app>
</template>

<script setup lang="ts">

const pageTitle = ref('little en grey')

useSeoMeta({
    title: pageTitle,
    ogTitle: pageTitle,
    description: 'ポートフォリオサイトです',
    ogDescription: 'ポートフォリオサイトです',
    // ogImage: '/IMG_3066.jpg',
    // twitterCard: 'summary_large_image',
});

</script>

<style>
html {
    font-family: 'Noto Sans JP', sans-serif;
}
</style>
