<template>
    <v-row justify="center" align="center">
        
    </v-row>
</template>

<script>
export default {
    name: 'SplatoonIndex',
    layout: 'game',
    data() {
        return {
            gameItems: [
                {
                    icon: 'mdi-twitter',
                    title: 'Twitter',
                    url: 'https://twitter.com/katsuo3130',
                },
                {
                    icon: 'mdi-youtube',
                    title: 'Youtube',
                    url: 'https://www.youtube.com/@katsuo3130',
                },
                {
                    icon: 'mdi-message-text-outline',
                    title: 'Misskey',
                    url: 'https://misskey.io/@katsuo3130',
                },
                {
                    icon: 'mdi-twitch',
                    title: 'Twitch',
                    url: 'https://www.twitch.tv/katsuo3130',
                },
                {
                    icon: 'mdi-instagram',
                    title: 'Instagram',
                    url: 'https://www.instagram.com/katsuo3130/',
                },
                {
                    icon: 'mdi-message-text-outline',
                    title: 'Threads',
                    url: 'https://www.threads.net/@katsuo3130',
                },
                {
                    icon: 'mdi-book-open-variant',
                    title: 'note',
                    url: 'https://note.com/katsuo3130',
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
