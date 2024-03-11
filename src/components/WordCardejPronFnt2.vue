<!-- playSound()で発話させる試み 機能：カードがクリックで日英反転し、対応する語が発話される-->
<!-- 左端のカードのeWordのみが発話される ${eWord}は通るが{{eWord}} はエラー-->
<template>
  <div class="card"
    :class="{bgImage: !flip, fgImage: flip}"
    @click="playSound(); flip=!flip"
  >
    <p :style="{fontSize:jfSize+'px', margin:0}" v-show="!flip">{{jWord}} </p>
    <p :style="{fontSize:efSize+'px', margin:0}" v-show="flip">{{eWord}} </p>
    <!-- ref="audio" autoplay は必須 v-showによる選択は効かない-->
    <!-- 後から定義(L13)した方の語が、クリックしたカードに対応して(flip状態に関係なく)発話される-->
    <audio :src="require('./../assets/evoice/'+eWord+'.mp3')" :id="'esound'+index"></audio>
    <audio :src="require(`./../assets/jvoice/${jWord}.mp3`)" :id="'jsound'+index"></audio>
    <img :src="require(`./../assets/fig/${eWord}.jpg`)" >

  </div>

</template>
<script>
export default {
  props: ["jWord", "eWord","index"],
  data(){
    return{
        flip: false,
    };
  },
  methods: {
    playSound(){
      // クリックしたカードではなく、左上のカードの音がflip状態に対応て出る。
        let se = document.getElementById("esound"+this.index)
        let sj = document.getElementById("jsound"+this.index)
        if (this.flip) {
            sj.play()
        } else {
            se.play()
        }
            
        }
  },
  created() {
    if (this.jWord.length > 3) {
       this.jfSize=180/this.jWord.length
    } else {
    this.jfSize=40
    }
    if (this.eWord.length > 8) {
       this.jfSize=180/this.eWord.length
    } else {
    this.efSize=40
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
  div.bgImage{
        background-image: url(./../assets/eCard.jpg);
        background-size: 200px;
  }
  div.fgImage{
        background-image: url(./../assets/jCard.jpg);
        background-size: 200px;
  }
    img {width: 200px;}
</style>
