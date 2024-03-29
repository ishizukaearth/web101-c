<!-- web101-ｃ AppTwoWordCard
    10枚のcard列表し、訳語読み上げ(WordCard)と1枚のカードの反復読み上げ(WordCardTimer)をflgで切り替える
    切り替えがうまくいかない！！
-->

<template>
    <div id="app">
        <div flg="false"></div>
        <!-- flg="false" --> 
        <div v-if="flg">
            <!-- 訳語 -->
            <WordCard v-for="(c, index) in cards" :key="index" :jWord="c.jWord" :eWord="c.eWord" :index="index"></WordCard>
        </div>
        <div v-else>
            <!-- 反復 -->
            <WordCardTimer v-for="(c, index) in cards" :key="index" :jWord="c.jWord" :eWord="c.eWord" :index="index"></WordCardTimer>
        </div>
    </div>
</template>

<script>
import WordCard from "./components/WordCardPron.vue"
import WordCardTimer from "./components/WordCardPronTimer.vue"
// flg=true
// jsonフィルの読み込み
// 出典 https://pystyle.info/vue-load-json-data-statically-and-dynamically/
import wordData from "./assets/wordData.json";
console.log(wordData)
// waorDataは10要素のarrayとして正しく読み込まれている
export default {
    name: "App",
    components: {
        WordCard,
        WordCardTimer,
    },
    data() {
        return {
            cards: [],
        };
    },

    created() {
        this.cards = [];
        for (var j = 0; j < wordData.length; j++) {
            this.cards.push({ jWord: wordData[j].jWord, eWord: wordData[j].eWord });
        }
        // カードの並べ順をランダム化
        // while (temp.length >0 ) {
        //     var r= Math.floor(Math.random() * temp.length);
        //     this.cards.push(temp[r]);
        //     temp.splice(r,1);
        // }
    },
}
</script>