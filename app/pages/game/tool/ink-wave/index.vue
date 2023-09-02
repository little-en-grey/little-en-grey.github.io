<template>
    <v-row justify="center" align="center">
        <v-col cols="12" sm="8" md="6">
            <v-card>
                <v-card-title class="headline">
                    Profile Maker
                </v-card-title>
                <v-card-text>
                    <v-row justify="start">
                        <!-- 名前 -->
                        <v-col cols="12">
                            <v-text-field v-model="inputName" id="input-name" placeholder="10文字以内" name="name"
                                maxlength="10" label="Name"></v-text-field>
                        </v-col>

                        <!-- 年齢 -->
                        <v-col cols="6">
                            <v-text-field v-model="inputAge" id="input-age" class="form-control" name="age" maxlength="2"
                                label="Age"></v-text-field>
                        </v-col>

                        <!-- 性別 -->
                        <v-col cols="6">
                            <v-select v-model="selectGender" :items="genderData" item-text="name" item-value="id"
                                density="compact" label="Gender"></v-select>
                        </v-col>


                        <!-- ボイスチャット -->
                        <v-col cols="12">
                            <v-select v-model="selectVoiceChat" :items="vcData" item-text="name" item-value="id"
                                density="compact" chips multiple label="VC"></v-select>
                        </v-col>

                        <!-- XP -->
                        <v-col cols="12">
                            <v-text-field type="text" v-model="inputXpArea" id="input-area" class="form-control" name="area"
                                maxlength="6" label="エリア"></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field type="text" v-model="inputXpYagura" id="input-yagura" class="form-control"
                                name="yagura" maxlength="6" label="ヤグラ"></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field type="text" v-model="inputXpHoko" id="input-hoko" class="form-control" name="hoko"
                                maxlength="6" label="ホコ"></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field type="text" v-model="inputXpAsari" id="input-asari" class="form-control"
                                name="asari" maxlength="6" label="アサリ"></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field type="text" v-model="inputXpFes" id="input-fes" class="form-control" name="fes"
                                maxlength="6" label="ナワバリ"></v-text-field>
                        </v-col>

                        <!-- ブキ -->
                        <v-col cols="12">
                            <v-textarea label="Weapon" v-model="inputWeapon" hint="改行不可/85文字まで" maxlength="85"></v-textarea>
                        </v-col>


                        <!-- Range -->
                        <v-col cols="12" sm="6">
                            <v-select v-model="selectRange" :items="rangeData" item-text="name" item-value="id"
                                density="compact" label="Range"></v-select>
                        </v-col>

                        <!-- 役割 -->
                        <v-col cols="12" sm="6">
                            <v-select v-model="selectRole" :items="roleData" item-text="name" item-value="id"
                                density="compact" label="Role"></v-select>
                        </v-col>

                        <!-- 参加曜日 -->
                        <v-col cols="12">
                            <v-select v-model="selectLeagueDate" :items="dateData" item-text="name" item-value="id"
                                density="compact" chips multiple label="League Date"></v-select>
                        </v-col>

                        <!-- メモ -->
                        <v-col cols="12">
                            <v-textarea label="Memo" v-model="inputMemo" hint="改行不可/272文字まで" maxlength="272"></v-textarea>
                        </v-col>

                        <canvas ref="imageCanvas" class="confirm-image" :width="canvasWidth"
                            :height="canvasHeight"></canvas>
                        <a :download="imageName" :href="imageDataURL" v-if="imageDataURL">Download Image</a>
                    </v-row>
                </v-card-text>
                <v-card-actions>
                    <v-spacer />
                    <v-btn color="primary" @click="generateImage"> Generate Image </v-btn>
                </v-card-actions>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
export default {
    name: 'IndexPage',
    data() {
        return {
            // 入力項目
            inputName: '',          // 名前
            inputAge: '',           // 年齢
            selectGender: '0',      // 性別
            selectVoiceChat: [],    // VC
            inputXpArea: '',        // XP（エリア）
            inputXpYagura: '',      // XP（ヤグラ）
            inputXpHoko: '',        // XP（ホコ）
            inputXpAsari: '',       // XP（アサリ）
            inputXpFes: '',         // フェスパワー
            inputWeapon: '',        // 使用ブキ
            selectRange: [],        // 範囲
            selectRole: [],         // 役割
            selectLeagueDate: [],   // 参加リーグ曜日
            inputMemo: '',          // メモ

            genderData: [
                { 'id': 0, 'name': '非公開' },
                { 'id': 1, 'name': '男性' },
                { 'id': 2, 'name': '女性' },
            ],
            vcData: [
                { 'id': 1, 'name': 'Discord' },
                { 'id': 2, 'name': 'LINE' },
                { 'id': 3, 'name': 'Nintendo Switch' },
                { 'id': 0, 'name': 'None' },
            ],
            rangeData: [
                { 'id': 1, 'name': 'SHORT' },
                { 'id': 2, 'name': 'MIDDLE' },
                { 'id': 3, 'name': 'LONG' },
            ],
            roleData: [
                { 'id': 1, 'name': 'ATTACKER' },
                { 'id': 2, 'name': 'SUPPORTER' },
                { 'id': 3, 'name': 'CONTROLLER' },
                { 'id': 4, 'name': 'TANKER' },
                { 'id': 5, 'name': 'MEGAPHONE RUNNER' },
                { 'id': 6, 'name': 'BALANCER' },
            ],
            dateData: [
                { 'id': 1, 'name': 'MON' },
                { 'id': 2, 'name': 'WED' },
                { 'id': 3, 'name': 'FRI' },
            ],

            imageDataURL: null,
            imageName: 'generated_image.png',
            baseImageUrl: '/card.png', // ベース画像のURLを設定
            canvasWidth: 1080, // キャンバスの幅
            canvasHeight: 1920 // キャンバスの高さ
        };
    },
    methods: {
        generateImage() {
            const canvas = this.$refs.imageCanvas;
            console.log(canvas);
            if (!canvas || !canvas.getContext) return false;

            const context = canvas.getContext('2d');

            // Draw base image
            const baseImage = new Image();
            baseImage.src = this.baseImageUrl;
            baseImage.onload = () => {
                context.drawImage(baseImage, 0, 0, this.canvasWidth, this.canvasHeight);

                // Draw text
                context.fillStyle = 'white';
                context.font = '30px Arial';

                // 円描画用
                context.strokeStyle = "white";
                context.lineWidth = 5;

                // 入力された内容は指定の位置に配置
                context.fillText(this.inputName, 100, 375);
                context.fillText(this.inputAge, 100, 535);
                context.fillText(this.inputXpArea, 100, 740);
                context.fillText(this.inputXpYagura, 285, 740);
                context.fillText(this.inputXpHoko, 480, 740);
                context.fillText(this.inputXpAsari, 670, 740);
                context.fillText(this.inputXpFes, 860, 740);

                const weaponLines = this.inputWeapon.replace(/\n/g, '　').match(/.{1,17}/g) || [];
                let lineHeight = 40;

                for (let i = 0; i < (weaponLines.length > 5 ? 5 : weaponLines.length); i++) {
                    context.fillText(weaponLines[i], 100, 882 + i * lineHeight);
                }

                context.font = '26px Arial';
                const memoLines = this.inputMemo.replace(/\n/g, '　').match(/.{1,34}/g) || [];
                lineHeight = 35;

                for (let i = 0; i < (memoLines.length > 8 ? 8 : memoLines.length); i++) {
                    context.fillText(memoLines[i], 100, 1587 + i * lineHeight);
                }

                // Gender描画
                let genderX;
                const genderY = 510;
                context.beginPath();
                switch (this.selectGender) {
                    case '0':
                        genderX = 400;
                        break;
                    case '1':
                        genderX = 305;
                        break;
                    case '2':
                        genderX = 485;
                        break;
                }
                context.arc(genderX, genderY, 40, 0 * Math.PI / 180, 360 * Math.PI / 180, false);
                context.stroke();

                // VC描画
                const vcX = { "0": 944, "1": 630, "2": 732, "3": 833 };
                const vcY = 514;
                this.selectVoiceChat.forEach(item => {
                    if (vcX[item] !== undefined) {
                        context.beginPath();
                        context.arc(vcX[item], vcY, 40, 0 * Math.PI / 180, 360 * Math.PI / 180, false);
                        context.stroke();
                    }
                });

                // Range描画
                const rangeX = 853
                let rangeY;
                context.beginPath();
                switch (this.selectRange) {
                    case '1':
                        rangeY = 875;
                        break;
                    case '2':
                        rangeY = 949;
                        break;
                    case '3':
                        rangeY = 1027;
                        break;
                }
                context.ellipse(rangeX, rangeY, 80, 25, 0, 0, 2 * Math.PI, false);
                context.stroke();

                // Role描画
                let roleX
                const roleY = 1200;
                context.beginPath();
                switch (this.selectRole) {
                    case '1':
                        roleX = 153;
                        break;
                    case '2':
                        roleX = 308;
                        break;
                    case '3':
                        roleX = 461;
                        break;
                    case '4':
                        roleX = 617;
                        break;
                    case '5':
                        roleX = 771;
                        break;
                    case '6':
                        roleX = 927;
                        break;
                }
                context.arc(roleX, roleY, 60, 0 * Math.PI / 180, 360 * Math.PI / 180, false);
                context.stroke();

                // League Date描画
                const dateX = { "1": 254, "2": 541, "3": 826 };
                const dateY = 1420;
                this.selectLeagueDate.forEach(item => {
                    if (dateX[item] !== undefined) {
                        context.beginPath();
                        context.ellipse(dateX[item], dateY, 80, 25, 0, 0, 2 * Math.PI, false);
                        context.stroke();
                    }
                });

                // Update image data URL
                this.imageDataURL = canvas.toDataURL();
            };
        }
    },
}
</script>

<style scoped>
.checkbox-container {
    display: flex;
    gap: 10px;
    /* チェックボックス間の間隔を設定 */
}

.confirm-image {
    width: 100%;
    height: auto;
}
</style>
