<template>
    <div>
        <v-row justify="start">
            <!-- 人数 -->
            <v-col cols="12">
                <v-select
                    v-model="selectNumber"
                    :items="maxCount"
                    density="compact"
                    label="人数"
                ></v-select>
            </v-col>
        </v-row>
        <v-row justify="start">
            <!-- 参加者名 -->
            <v-col v-for="n in selectNumber" :key="n" cols="6">
                <v-text-field v-model="playerName[n-1]" :label="'参加者' + n"></v-text-field>
            </v-col>

            <!-- ブキカテゴリ -->
            <v-col cols="12">
                <v-select
                    v-model="selectCategory"
                    :items="allCategoriesData"
                    item-text="name"
                    item-value="id"
                    density="compact"
                    label="ブキカテゴリ"
                ></v-select>
            </v-col>

            <!-- サブ -->
            <v-col cols="12">
                <v-select
                    v-model="selectSubWeapon"
                    :items="allSubWeaponsData"
                    item-text="name"
                    item-value="id"
                    density="compact"
                    label="サブウェポン"
                ></v-select>
            </v-col>

            <!-- スペシャル -->
            <v-col cols="12">
                <v-select
                    v-model="selectSpesialWeapon"
                    :items="allSpesialWeaponsData"
                    item-text="name"
                    item-value="id"
                    density="compact"
                    label="スペシャルウェポン"
                ></v-select>
            </v-col>

            <!-- ウェブフック -->
            <v-col cols="12" class="md-1">
                <v-checkbox
                    v-model="checkSendDiscord"
                    label="Discordに結果を送信"
                ></v-checkbox>
                
            </v-col>
            <v-col cols="6">
                <v-btn @click="sendTest()">テスト送信</v-btn>
            </v-col>
            <v-col cols="12">
                <v-text-field v-model="webhookUrl" :label="'Webhook URL'"></v-text-field>
            </v-col>

            <v-col cols="12">
                <v-btn @click="getRandomData()">ルーレットスタート!!</v-btn>
            </v-col>

            <!-- ランダムに取得したデータを表示 -->
            <template v-for="(item, index) in randomData" >
                <v-col :key="index" cols="12" sm="8" md="6"
                >   {{ displayPlayerName[index] ?? '参加者' + (index + 1) }} ： {{ item.name }}
                </v-col>
            </template>
        </v-row>

        <v-snackbar
            v-model="snackbarFlag"
        >
            {{ text }}

            <template v-slot:action="{ attrs }">
                <v-btn
                color="pink"
                text
                v-bind="attrs"
                @click="snackbarFlag = false"
                >
                Close
                </v-btn>
            </template>
        </v-snackbar>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'SplatoonRandom',
    layout: 'game',
    async asyncData() {
        const weapons = await import('@/static/spla/main_weapons.json');
        const subWeapons = await import('@/static/spla/sub_weapons.json');
        const spesialWeapons = await import('@/static/spla/special_weapons.json');
        const categories = await import('@/static/spla/categories.json');

        return { 
            allWeaponsData: weapons.default,
            allSubWeaponsData: subWeapons.default,
            allSpesialWeaponsData: spesialWeapons.default,
            allCategoriesData: categories.default,
        };
    },
    data() {
        return {
            maxCount: [...Array(9).keys()].slice(1),
            selectNumber: 8,
            selectCategory: 0,
            selectSubWeapon: 0,
            selectSpesialWeapon: 0,
            playerName: [],
            displayPlayerName: [],
            randomData: [], // ランダムに抽出した8つのデータを格納する配列
            webhookUrl: null,
            checkSendDiscord: false,
            snackbarFlag: false,
            text: "送信完了！",
        }
    },
    
    methods: {
        getRandomData() {
            this.displayPlayerName = this.playerName.slice();

            // 条件に基づいてデータをフィルタリングする
            let filteredData = this.allWeaponsData;

            // subItemが指定されている場合、該当するデータを抽出
            if (this.selectSubWeapon) {
                filteredData = filteredData.filter(item => item.sub === this.selectSubWeapon);
            }

            // specialが指定されている場合、該当するデータを抽出
            if (this.selectSpesialWeapon) {
                filteredData = filteredData.filter(item => item.special === this.selectSpesialWeapon);
            }

            // categoryが指定されている場合、該当するデータを抽出
            if (this.selectCategory) {
                filteredData = filteredData.filter(item => item.category === this.selectCategory);
            }

            // ランダムに8つのデータを抽出する
            this.randomData = this.getRandomItems(filteredData, this.selectNumber);

            // webhookがあれば送信
            if(this.checkSendDiscord) {
                this.sendDiscord(false);
            }
        },

        // ランダムにデータを抽出するヘルパー関数
        getRandomItems(arr, num) {
            const data = [];
            const length = arr.length;

            for (let i = 0; i < num; i++) {
                const index = Math.floor(Math.random() * length);
                data.push(arr[index]);
            }
            return data;
        },

        sendTest() {
            if(this.checkSendDiscord) {
                if(this.webhookUrl) {
                    this.sendDiscord(true);
                } else {
                    this.snackbarFlag = true;
                    this.text = "URLが入力されていません";
                }
            } else {
                this.snackbarFlag = true;
                this.text = "送信するにチェックがありません";
            }
        },

        sendDiscord(sendTest) {
            let contents = "";
            if(sendTest) {
                contents = 'これはテスト送信です!!';
            } else {
                contents = "◇武器ルーレット\n```";
                for(let i=0;i<this.randomData.length;i++) {
                    contents += (this.displayPlayerName[i] ?? '参加者' + (i + 1)) + " ： " + this.randomData[i].name + "\n";
                    console.log(this.randomData[i].name);
                }
                contents += "``` ----------";
            }

            const message = {
                "content": contents,
            }

            axios.post(this.webhookUrl, message)
                .then(response => {
                    console.log('Message sent:', response.data);
                    this.snackbarFlag = true;
                    this.text = "送信に成功しました";
                })
                .catch(error => {
                    console.error('Error sending message:', error);
                    this.snackbarFlag = true;
                    this.text = "送信に失敗しました";
                });
        }
    }
}
</script>