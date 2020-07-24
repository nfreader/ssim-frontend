<template>
  <div id="app">
    <Header v-bind:year="year" />
    <div id="game" class="ph2 pv1">
      <router-view/>
    </div>
    <Footer v-bind:name="name" v-bind:version="version" />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Header,
    Footer
  },
  data: function() {
    return {
      year: '',
      name: 'Space Sim',
      version: '1.0.0'
    };
  },
  methods: {
    getInfo() {
      axios.get('http://localhost:8000/api/game/info').then(res=> {
        console.log(res.data)
        this.year = res.data.year
        this.name = res.data.name
        this.version = res.data.version
      }).catch(err => {
        console.log(err)
      });
    }
  },
  created() {
    this.getInfo()
  }
}
</script>
