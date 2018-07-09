<template>
  <div id="app">
    <img src="https://oscarpallas.github.io/platzimusic/dist/logo.png">
    <h1>{{ msg }}</h1>
    <select v-model="selectedCountry">
      <option v-for="c in countries" :value="c.value"> {{ c.name }} </option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="a in artists" v-bind:a="a" v-bind:key="a.mbid"></artist>
    </ul>
  </div>
</template>

<script>
import spinner from './components/Spinner.vue'
import artist from './components/Artist.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      msg: 'Platzimusic',
      artists: [],
      countries: [
          {
            name: 'España', value: 'spain'
          },
          {
            name: 'Grecia', value: 'greece'
          },
          {
            name: 'Reino Unido', value: 'united kingdom'
          }
      ],
      selectedCountry: 'spain',
      loading: true
    }
  },
  components: {
    artist,
    spinner
  },
  methods: {
      refreshArtists(){
          this.loading = true
          const _this = this
          this.artists = []
          getArtists(this.selectedCountry).then(function(artists){
            _this.loading = false
            _this.artists = artists
          })
      }
  },
  mounted(){
    this.refreshArtists()
  },
  watch: {
    selectedCountry(){
        this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
#app 
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
h1, h2 
  font-weight normal
ul 
  list-style-type none
  padding 0
li 
  display inline-block
  margin 0 10px
a 
  color #42b983
</style>
