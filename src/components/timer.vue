<template>
  <div class="tim">
    <div class="days cont">
      <NUMC :num="0" :newnum="days" />
      <h3>DAYS</h3>
    </div>
    <div class="hours cont">
      <NUMC :num="0" :newnum="hours"/>
      <h3>HOURS</h3>
    </div>
    <div class="minutes cont">
      <NUMC :num="0" :newnum="minutes"/>
      <h3>MINUTES</h3>
    </div>
    <div class="seconds cont">
      <NUMC :num="0" :newnum="seconds"/>
      <h3>SECONDS</h3>
    </div>
  </div>
</template>

<script>
import NUMC from "./number.vue"
  export default{
    name:"TIMER",
    components:{
      NUMC,
    },
    data(){
      return{
        days:0,
        hours:0,
        minutes:5,
        seconds:0,
        datum: new Date('february 25, 2023 010:00:00'),
      }
    },
    methods:{
      dajDatum(){
        const currentDate = new Date()
        const time = Math.ceil((this.datum - currentDate) / 1000)
        this.seconds = time % 60
        this.minutes = Math.floor(time / 60) % 60
        this.hours = Math.floor(time / 3600) %24
        this.days = Math.floor(time / 3600 / 24)
      }
    },
    created(){
      setInterval(() => {
        this.days +=1
        this.dajDatum()
      }, 1000);
    }
  }
</script>

<style scoped>
  .tim{
    display: flex;
    width: 720px;
    justify-content: space-between;
  }
  .cont{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  h3{
    font-size: 14px;
    color:hsl(237, 18%, 59%);
    padding-left: 6px;
  }
</style>