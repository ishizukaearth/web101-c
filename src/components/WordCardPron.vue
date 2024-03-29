<!-- クリックしたカードが日英反転し、反転後の言語で読み上げる -->
<!-- -->
<template>
  <div class="card"
    :class="{bgImage: !flip, fgImage: flip}"
    @click="playSound(); flip=!flip"
  >
    <p :style="{fontSize:jfSize+'px', margin:0}" v-show="!flip">{{jWord}} </p>
    <p :style="{fontSize:efSize+'px', margin:0}" v-show="flip">{{eWord}} </p>
    <p>-訳語-</p>
  
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
        let se = document.getElementById("esound"+this.index)
        let sj = document.getElementById("jsound"+this.index)
        if (this.flip) {
            se.play()
        } else {
            sj.play()
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
