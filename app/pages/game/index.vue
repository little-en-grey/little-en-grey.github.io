<template>
  <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6">
        <a v-for="(item, i) in gameItems" :key="i" :href="item.url" target="_blank" rel="noopener noreferrer">
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
  name: 'GameIndexPage',
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
