<template>
  <header id="game_header" class="">
    <span><i class="fa fa-satellite-dish"></i> S.I.M.S.</span>
    <span id="game_clock">{{date}}</span>
    <!-- <nav id="globalnav">
      <router-link to="/" class="link dib white hover-black hover-bg-white pa1"><span class="f7 green">sys.</span>Vessel</router-link>
      <router-link to="/navigation" class="link dib white hover-black hover-bg-white pa1"><span class="f7 green">sys.</span>Navigation</router-link>
    </nav> -->
  </header>
</template>

<script>
import moment from 'moment'
export default {
  props:['year'],
  data:()=>{
    return {
      date: ''
    }
  },
  methods: {
    getGameDate() {
      return moment().add(this.year, "years").utc().format("HH:mm:ss DD.MM.YYYY")
    }
  },
  created() {
    this.date = this.getGameDate()
    var seps = true;
    this.clock = setInterval(() => {
      if(seps) {
        this.date = this.getGameDate().replace(/:/g,' ')
        seps = false
      } else {
        this.date = this.getGameDate()
        seps = true
      }
    }, 1000);
  }
  
}

</script>