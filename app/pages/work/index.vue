<template>
    <v-row justify="center" align="center">
        <v-col cols="12" sm="8" md="6">

            <a v-for="(item, i) in workItems" :key="i" :href="item.url" target="_blank" rel="noopener noreferrer">
                <v-card class="mb-3">
                    <v-list-item three-line>
                        <v-icon x-large color="grey" class="mr-3">{{ item.icon }}</v-icon>
                        <v-list-item-content>
                            <v-list-item-title class="text-h6 mb-1">
                                {{ item.title }}
                            </v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-card>
            </a>
        </v-col>
    </v-row>
</template>



<script>
export default {
    name: 'WorkIndexPage',
    layout: 'work',
    data() {
        return {
            workItems: [
                {
                    icon: 'mdi-twitter',
                    title: 'Twitter',
                    url: 'https://twitter.com/little_en_grey',
                },
                {
                    icon: 'mdi-instagram',
                    title: 'Instagram',
                    url: 'https://www.instagram.com/little_en_grey/',
                },
                {
                    icon: 'mdi-book-open-variant',
                    title: 'note',
                    url: 'https://note.com/_little_en_grey/',
                },
                {
                    icon: 'mdi-github-circle',
                    title: 'Github',
                    url: 'https://github.com/little-en-grey/',
                },
            ],
        }
    },
}
</script>

<style>
a {
    text-decoration: none;
}
</style>