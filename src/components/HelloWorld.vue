<template>
<div>
  <input type="text" @keyup="movieSearch" v-model="inputValue">
  <select name="" id="" v-model="searchType" @click="movieSearch">
    <option value="movie" selected >movie</option>
    <option value="series">series</option>
    <option value="episode">episode</option>
  </select>
  <ul>
    <li v-bind:key="movie.imdbID" v-for="movie in movieList" v-if="typeSelected">
      <img :src="movie.Poster" alt="">
      <h4>{{movie.Title}}</h4>
      <p>{{movie.Year}}</p>
      <p>{{movie.Type}}</p> 
    </li>
  </ul>
</div>
</template>

<script>
export default {
  name: 'HelloWorld',

  methods:{
    movieSearch(){
      this.axios.get('http://www.omdbapi.com/?s='+ this.inputValue + '&apikey=234d140c' + '&type='+ this.searchType).then(response => { this.movieList = response.data.Search
      })
    },
    typeSelected(){
      if(this.searchType !== ""){
        return this.movie.Type == this.searchType;
      }else{
        return true;
      }

    }

  },

  data(){
    return {
      
      inputValue:"",
      movieList:"",
      searchType: ''

    }
  }
 }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h3 {
  margin: 40px 0 0;
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
