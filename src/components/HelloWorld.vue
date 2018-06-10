<template>
<div>
  <input type="text" @keyup="movieSearch" v-model="inputValue">
  <select name="" id="select" v-model="searchType" @click="movieSearch">
    <option value="movie" selected >movie</option>
    <option value="series">series</option>
    <option value="episode">episode</option>
  </select>
  <ul>
    <li v-bind:key="movie.imdbID" v-for="movie in movieList" v-if="typeSelected">
      <img :src="movie.Poster" alt="">
      <div class="searchResults">
        <h4>{{movie.Title}}</h4>
        <p>{{movie.Year}}</p>
        <p>Type: {{movie.Type}}</p> 
        <hr>
      </div>
     
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
<style  lang='scss'>
input {
  font-size: 45px;
  padding: 10px;
  width: 35%;
  border: 2px solid #29E7CD;
  border-radius: 15px;
}
#select {
    font-size: 25px;
    padding: 10px;
    border: 2px solid #29E7CD;
    display: block;
    margin: 20px auto;
    width: 20%;
    option {
      text-align: center;
    }
}
ul {
  display: grid;
  width: 60%;
  padding: 0;
  margin: 30px auto;
  grid-template-columns: repeat(3, 1fr);
    li {
    list-style-type: none;
    padding: 0px;
      img {
        margin-top: 20px;
        border-radius: 5px;
        height: 300px;
      }
      h4 {
        font-size: 25px;
        color: #A188A6;
      }
      p {
        font-size: 20px;
        margin: 5px;
        color: white;
      }
    }
    hr {
      color: #A188A6;
      margin: 30px 0;
      border-color: pink;
    }
}

</style>
