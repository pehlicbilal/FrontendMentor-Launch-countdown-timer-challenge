<template>
  <div class="card" ref="card" @flip="flip(newnum)">
    <div v-if="ast" class="topflip" ref="topflip" @animationstart="astart(newnum)" @animationend="atend">{{ topflip}}</div>
    <div class="top" ref="top">{{ topH }}</div>
    <div class="bottom" ref="bottom">{{bottomH }}</div>
    <div v-if="asb" class="bottomflip" ref="bottomflip" @animationend="aend(newnum)">{{ bottomflip }}</div>
  </div>
</template>

<script>
  export default{
    name: "NUMC",
    props:{
      num:Number,
      newnum:Number
    },
    emits:[
      "flip"
    ],
    data(){
      return{
        ast:false,
        asb:false,
        topflip:"00",
        bottomflip:"00",
        topH:"00",
        bottomH:"00",
      }
    },
    mounted() {
      this.$refs.top.value
    },
    methods:{
      flip(newnum){
        let snum = this.$refs.top.textContent
        if (newnum === parseInt(snum)) return
        this.ast = true
        this.asb = true
        this.bottomH= snum.toString().padStart(2, '0')
        this.topflip = snum.toString().padStart(2, '0')
        this.bottomflip = newnum.toString().padStart(2, '0')
      },
      astart(newnum){
        this.topH = newnum.toString().padStart(2, '0')
      },
      atend(){
        this.ast = false
      },
      aend(newnum){
        this.bottomH = newnum.toString().padStart(2, '0')
        this.asb = false
      }
    },
    created(){
      setInterval(() => {
        this.flip(this.newnum)
      }, 1000);
    }
  }
</script>

<style scoped>
  *, *::after, *::before {
  box-sizing: border-box;
}
  .card{
    background: #1A1A25;
    height: 135px;
    width: 155px;
    border-radius: 6px;
    position: relative;
    display: inline-flex;
    flex-direction: column;
  }
  .top,.bottom,.topflip,.bottomflip{
    font-size: 64px;
    border-radius: 6px;
    height: 64px;
    line-height: 1;
    padding: 32px 16px 32px 16px;
    overflow: hidden;
    justify-content: center;
  }
  .top,.topflip{
    
    z-index: 0;
    color:#D54F6F;
    background: #2D2D44;
    border-bottom: 0.1px solid #1A1A25; 
    --mask: radial-gradient(7px at 7px 100%,#0000 98%,#000) -7px;
    -webkit-mask: var(--mask);
          mask: var(--mask);
  }
  .bottom,.bottomflip{
    z-index: 0;
    color:#F85E85;
    background: #35374F;
    display: flex;
    align-items: flex-end;
    --mask: radial-gradient(7px at 7px 0,#0000 98%,#000) -7px;
    -webkit-mask: var(--mask);
          mask: var(--mask);
  }
  .card .topflip{
    z-index: 1;
    position:absolute;
    width:100%;
    transform-origin: bottom;
    animation: flopD 250ms ease-in;
  }
  .card .bottomflip{
    z-index: 1;
    position:absolute;
    bottom: 6px;
    width:100%;
    transform-origin: top;
    animation: flopDD 250ms ease-out 250ms;
    transform: rotateX(90deg);
  }

  @keyframes flopD {
    100%{
      transform: rotateX(90deg);
    }
  }
  @keyframes flopDD {
    100%{
      transform: rotateX(0deg);
    }
  }
</style>