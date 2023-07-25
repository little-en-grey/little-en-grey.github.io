<template>
    <v-row justify="center" align="center">
        <v-container>
            <v-row>
                <v-col
                    v-for="n in maxCount"
                    :key="n"
                    cols="6"
                >
                    <v-text-field :label="'name' + n"></v-text-field>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12">
                    <v-btn outlined>ルーレットスタート！</v-btn>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12">
                    <v-btn outlined>ルーレットスタート！</v-btn>
                </v-col>
            </v-row>
        </v-container>
    </v-row>
</template>

<script>
export default {
    name: 'RandomWepons',
    data() {
        return {
            maxCount: 8,
            selectCategory: 0,
            mainWeapon: "main",
            textData:"",
            countNum:1,
            resultWrapons: [],
            userNames: [],
            playerName: [],
            flag: false,
            itemData: [],
        }
    },
}
</script>