<template lang="html">
  <div class="searchMovie">
    <form
      v-if="showForm"
      v-on:submit.prevent="onSubmit">
        <input
        type="text"
        placeholder="a movie to argue about"
        v-show="showForm"
        v-model="movie_name">
        <input
        type="submit"
        value="👊"
        v-show="showForm"
        v-on:keyup.enter="submit">
    </form>
    <chooseMovie v-if="showList" v-bind:api_res_movie_list="api_res_movie_list"></chooseMovie>
  </div>
</template>

<script>
  import axios from 'axios'
  import chooseMovie from './chooseMovie'

  export default {
    name: 'searchMovie',
    components: {
      chooseMovie
    },
    data () {
      return {
        showForm: true,
        showList: false,
        movie_name: '',
        TMDB_api_key: '3afb334973093028cc5d28d0464b6383',
        api_res_movie_list: ''
      }
    },
    methods: {
      onSubmit: function () {
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${this.TMDB_api_key}&language=en-US&query=${this.movie_name}&page=1&include_adult=false`)
          .then(res => {
            const movieList = res.data.results.slice(0, 5)
            if (movieList.length === 0) {
              alert('nothing found :(')
              // this.reload()
            } else {
              this.api_res_movie_list = movieList
            }
          })
          .then(() => {
            this.showForm = false
            this.showList = true
          })
          .catch(err => this.reload())
      },
      reload: function () {
        this.movie_name = ''
        this.showForm = true
        this.showList = false
      }
    }
  }
</script>

<style lang="css">
h1 {
  font-size: 4em;
  font-weight: bold;
text-shadow: 1px 1px 4px rgba(150, 150, 150, 0.98);
cursor: pointer;
}
input {
  font-size: 2em;
}
</style>
