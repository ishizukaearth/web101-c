<!-- playSound()で発話させる試み -->
<!-- 左端のカードのeWordのみが発話される ${eWord}は通るが{{eWord}} はエラー-->
<template>
  <div class="card"
    :class="{bgImage: !flip, fgImage: flip}"
    @click="playSound(); flip=!flip"
  >
    <p :style="{fontSize:jfSize+'px', margin:0}" v-show="!flip">{{jWord}} </p>
    <p :style="{fontSize:efSize+'px', margin:0}" v-show="flip">{{eWord}} </p>
    <audio :src="require(`./../assets/evoice/${eWord}.mp3`)" id="sound"></audio>
    <!-- <audio :src="'./../assets/'+${eWord}+'.wav`" id="sound"></audio> -->
  </div>

</template>
<script>
export default {
  props: ["jWord", "eWord"],
  data(){
    return{
        flip: false,
    };
  },
  methods: {
    playSound(){
            let s = document.getElementById("sound")
            s.play()
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
    height: 100px;
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
