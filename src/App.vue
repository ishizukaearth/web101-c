<!-- web101-b 
    １．単語データをファイルから読み込む GetWords.vue
    ２．英文字の頭文字を切り出す
-->
<!-- コメントたりとも全角空白はエラーとなる -->
<template>
    <div id="app">    
        <WordCard
            v-for="(c,index) in cards"
            :key="index"
            :jWord="c.jWord"
            :eWord="c.eWord"
            :index="index"
        ></WordCard>
    </div>
</template>
<script>
import WordCard from "./components/WordCardejPronFnt2.vue";
// jsonフィルの読み込み
// 出典 https://pystyle.info/vue-load-json-data-statically-and-dynamically/
// import wordData from "./assets/wordData.json";
// console.log(wordData)
// waorDataは10要素のarrayとして正しく読み込まれている
export default {
    name: "App",
    components:{
        WordCard,
    },
    data() {
        return {
            cards: [],
        };
    },

    created(){
        // ファイルがjson形式でないとのエラーが出るので直に定義してみた
        var wordData = [
        {
            "eWord": "cat",
            "jWord": "猫"
        },
        {
            "eWord": "catch",
            "jWord": "捕まえる"
        },
        {
            "eWord": "hat",
            "jWord": "帽子"
        }]
        console.log(wordData)
        // waorDataは3要素のarrayとして正しく読み込まれている
        var words=  JSON.parse(wordData)
        /* ** error ***
          SyntaxError: Unexpected token 'o', wordData is not valid json " 
          しかし、https://jsonlint.com/の判定ではjson is valid
        */
        this.cards=[];
            for (var j=0;j<wordData.length;j++){
                this.cards.push({jWord: words[j].jWord, eWord: words[j].eWord});
            }

        // while (temp.length >0 ) {
        //     var r= Math.floor(Math.random() * temp.length);
        //     this.cards.push(temp[r]);
        //     temp.splice(r,1);
        // }
    },
}
</script>