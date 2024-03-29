<!-- クリックしたカードを翻訳語日英反復読上げる Mar 28 -->
<!-- 0.第1語の発話が遅れる：クリック後にse,sjを設定するlatencyが原因か 
       → a,発話時刻の表示、b.sj,seをあらかじめ定義できないか
     1.発展：固定間隔でなく、発話完了後に次の語をやみ上げる
     2.音量のコントロール
-->

<template>
    <div class="card" :class="{ bgImage: !flip, fgImage: flip }" @click="start(); flip = !flip">
        <p :style="{ fontSize: jfSize + 'px', margin: 0 }" v-show="!flip">{{ jWord }} </p>
        <p :style="{ fontSize: efSize + 'px', margin: 0 }" v-show="flip">{{ eWord }} </p>
        <p>-反復-</p>
        <!-- indexはカード番号 -->
        <audio :src="require('./../assets/evoice/' + eWord + '.mp3')" :id="'esound' + index"></audio>
        <audio :src="require(`./../assets/jvoice/${jWord}.mp3`)" :id="'jsound' + index"></audio>
        <img :src="require(`./../assets/fig/${eWord}.jpg`)">
    </div>

</template>
<script>
let count = 0;
let timer = NaN;
// let se = document.getElementById("esound" + this.index) //ここで定義するとエラーになる
// let sj = document.getElementById("jsound" + this.index)
export default {
    props: ["jWord", "eWord", "index"],
    data() {
        return {
            flip: false,
        };
    },
    methods: {
        start() {
            clearInterval(timer);
            count = 0;
            timer = setInterval(this.ejPron, 700); // ejPronが未定義:thisが必要
            console.log("timer start: count=", count)
        },
        ejPron() {
            console.log("ejPron: count=", count)
            if (count > 3) {
                this.stop();
                return
            }
            let se = document.getElementById("esound" + this.index)
            let sj = document.getElementById("jsound" + this.index)
            if (count % 2 == 0) {
                if (this.flip) { sj.play() } else { se.play() }
            }
            else {
                if (this.flip) { se.play() } else { sj.play() }
            }
            count++;
        },
        stop() {
            clearInterval(timer);
        },
    },
    created() {
        if (this.jWord.length > 3) {
            this.jfSize = 180 / this.jWord.length
        } else {
            this.jfSize = 40
        }
        if (this.eWord.length > 8) {
            this.jfSize = 180 / this.eWord.length
        } else {
            this.efSize = 40
        }
    },
};
</script>

<style scoped>
div.card {
    display: inline-block;
    width: 200px;
    height: 300px;
    font-size: 40px;
    text-align: center;
    border: solid 1px black;
    border-radius: 10px;
    overflow: hidden;
}

div.bgImage {
    background-image: url(./../assets/eCard.jpg);
    background-size: 200px;
}

div.fgImage {
    background-image: url(./../assets/jCard.jpg);
    background-size: 200px;
}

img {
    width: 200px;
}
</style>
