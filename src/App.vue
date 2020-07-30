<template>
  <div id="app">
    <Header v-bind:year="game_year" />
    <div v-if="authenticated" id="game" class="ph2 pv1">
      <section id="game_sidebar" class="">
        <div id="sidebar_header">Stark Bledfast</div>
        <sidebar_header v-bind:name="name" v-bind:location="location"></sidebar_header>
        <nav id="main_nav" class="">
          <a class="main_nav_item"><i class="fas fa-fw fa-map-marker-alt f1"></i> <span class="">Navigation    </span></a>
          <a class="main_nav_item"><i class="fas fa-fw fa-space-shuttle f1"></i>  <span class="">Vessel </span></a>
          <a class="main_nav_item"><i class="fas fa-fw fa-th f1"></i>             <span class="">Cargo  </span></a>
          <a class="main_nav_item"><i class="fas fa-fw fa-bomb f1"></i>           <span class="">Weapons</span></a>
          <a class="main_nav_item"><i class="fas fa-fw fa-comment-alt f1"></i>    <span class="">Communications</span></a>
          <a class="main_nav_item"><i class="fas fa-fw fa-coins f1"></i>          <span class="">Banking</span></a>
          <a class="main_nav_item"><i class="fas fa-fw fa-address-card f1"></i>   <span class="">Profile</span></a>
        </nav>
      </section>
      <router-view/>
    </div>
    <div v-else>
      <Login />
    </div>
    <Footer v-bind:name="game_name" v-bind:version="game_version" />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import Login from '@/components/Login.vue'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Header,
    Footer,
    Login
  },
  data: function() {
    return {
      authenticated: false,
      game_year: '',
      game_name: 'Space Sim',
      game_version: '1.0.0'
    };
  },
  methods: {
    getInfo() {
      axios.get('http://localhost:8000/api/game/info').then(res=> {
        console.log(res.data)
        this.game_year = res.data.year
        this.game_name = res.data.name
        this.game_version = res.data.version
      }).catch(err => {
        console.log(err)
      });
    },
    getPilot() {
      if(this.authenticated){
        axios.get('http://localhost:8000/api/pilot').then(res=> {
          console.log(res.data)
        }).catch(err => {
          console.log(err)
        });
      }
    }
  },
  created() {
    this.getInfo()
    this.getPilot()
  }
}
</script>
