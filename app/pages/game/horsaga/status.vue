<template>
    <v-data-table :headers="headers" :items="allUnitData" item-value="name">

    </v-data-table>
</template>

<script>
export default {
    name: 'HorsagaStatus',
    layout: 'game',
    async asyncData() {
        const unit = await import('@/static/horsaga/unit_data.json');
        const attribute = await import('@/static/horsaga/attribute.json');
        const characteristic = await import('@/static/horsaga/characteristic.json');
        const knightSkill = await import('@/static/horsaga/knight_skill.json');
        const rarity = await import('@/static/horsaga/rarity.json');
        const skill = await import('@/static/horsaga/skill.json');
        const support = await import('@/static/horsaga/support.json');
        const tactics = await import('@/static/horsaga/tactics.json');

        return { 
            allUnitData: unit.default,
            allAttributeData: attribute.default,
            allCharacteristicData: characteristic.default,
            allKnightSkillData: knightSkill.default,
            allRarityData: rarity.default,
            allSkillData: skill.default,
            allSupportsData: support.default,
            allTacticsData: tactics.default,
        };
    },
    data() {
        return {
            search: '',
            headers: [
                { text: 'ID', value: 'id' },
                // { text: '肩書', value: 'title' },
                { text: '名前', value: 'name' },
                { text: 'レア', value: 'rarity' },
                { text: '属性', value: 'attribute' },
                { text: 'HP', value: 'health_point' },
                { text: '攻撃', value: 'attack' },
                { text: '防御', value: 'defense' },
                { text: '速度', value: 'speed' },
                { text: 'スキル', value: 'skills' },
                { text: 'UF', value: 'ultimate_force' },
                { text: 'タクティクス①', value: 'tactics_1' },
                { text: 'タクティクス②', value: 'tactics_2' },
                { text: '騎士スキル', value: 'knight_skill' },
                { text: '特性', value: 'characteristic' },
                { text: 'サポートスキル', value: 'support' },
                // { text: '備考', value: 'remarks' },
            ],
        }
    },
}
</script>