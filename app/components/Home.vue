<template>
    <v-row justify="center" class="mt-15 mb-5 mb-md-10">
        <v-col cols="12">
            <v-row justify="center" class="mt-15 mb-5 mb-md-10">
                <v-col cols="12" sm="8" md="6">
                    <div class="text-center text-h2 font-weight-bold" >{{ pageTitle }}</div>
                </v-col>
            </v-row>
        </v-col>

        <v-col cols="12">
            <v-row justify="center" class="mt-15 mb-5 mb-md-10">
                <v-col cols="12" sm="8" md="6">
                    <v-btn v-for="item in listItems" :key="item.title" block variant="outlined" rounded="sm" size="x-large"
                        class="text-none mb-4" :prepend-icon="item.icon" :color="item.color">
                        {{ item.title }}
                    </v-btn>
                </v-col>
            </v-row>
        </v-col>
    </v-row>
</template>

<script setup lang="ts">
import { LIST_ITEM } from '~/consts/list'

const pageTitle = ref('Welcome :)')
const listItems = LIST_ITEM
</script>

<style></style>
