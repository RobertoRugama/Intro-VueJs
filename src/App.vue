<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1> {{msg}}</h1>
    <div>
      <select v-model="selectedCountry">
        <option v-for ="country in countries" v-bind:value="country.value"> {{ country.name }}</option>
        option
      </select>  
      <spinner v-show="loading"></spinner>    
    </div>
    <ul>
      <artist v-for="artist in artists"
      v-bind:artist = "artist"></artist>
    </ul>    
  </div>
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'  
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome a Music Last.FM',

      artists: [],
      countries: [
        { name: 'Nicaragua', value:'Nicaragua'},
        { name: 'España', value:'Spain'},
        { name: 'Costa Rica', value: 'Costa Rica'},
        { name: 'Panama', value : 'Panama'},
        { name: 'Colombia', value : 'Colombia'},
        { name: 'Argentina', value : 'Argnetina'}

      ],
      selectedCountry: 'Nicaragua',
      loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods:{
    refreshArtists(){
    const self = this
    this.loading = true
    getArtists(this.selectedCountry)
      .then( function (artists) {
        self.loading = false
        self.artists = artists
      })
    }
  },
  mounted: function(){
    this.refreshArtists()
  },
  watch: {
    selectedCountry: function(){
      this.refreshArtists()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
