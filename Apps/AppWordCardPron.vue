<!-- web101-ｃ 
    目的
    単語データをファイル(wordData.josn)から読み込む（web101-b）を交互に連続読み上げたら、次の語へ進む
-->

<template>
    <div id="app">
        <WordCard v-for="(c, index) in cards" :key="index" :jWord="c.jWord" :eWord="c.eWord" :index="index"></WordCard>
    </div>
</template>

<script>
import WordCard from "./components/WordCardPron.vue"

// jsonフィルの読み込み
// 出典 https://pystyle.info/vue-load-json-data-statically-and-dynamically/
import wordData from "./assets/wordData.json";
console.log(wordData)
// waorDataは10要素のarrayとして正しく読み込まれている
export default {
    name: "App",
    components: {
        WordCard,
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