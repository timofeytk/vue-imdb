<template>
  <form @submit.prevent="SearchMovies">
      <input type="search" placeholder="Искать..." v-model="search">
      <input type="submit" value="Поиск">
  </form>
  <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <img :src="movie.image" alt="">
        <div class="movie-title">{{movie.title}}</div>
        <div class="movie-description">{{movie.description}}</div>
      </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import { API_URL } from '@/api'

export default {
  setup(){
      const search = ref("")
      const movies = ref([])

      const SearchMovies = () => {
          if(search.value !== ''){
              fetch(`${API_URL}/${search.value}`)
              .then(response => response.json())
              .then(data => {
                  movies.value = data.results;
                  search.value = '';
              })
          }
      }
      return {
          search,
          movies,
          SearchMovies
      }
  }

}
</script>

<style>
#app{
  max-width: 500px;
  margin: 0 auto;
}
.movies-list{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 0 15px;
}
.movie{
  margin-bottom: 15px;
  padding: 15px;
  border: 2px solid #26a4e3;
}
img{
  width: 100%;
  
}
.movie-title{
  text-align: center;
  font-size: 18px;
  margin: 15px auto;
  color: #333;
}
.movie-description{
  font-size: 14px;
  color: #333;
  text-align: center;
  margin: 0 auto;
}
form{
  display: flex;
  padding: 0 15px;
  margin-bottom: 1em;
}
input[type="search"]{
  border: none;
  border-bottom: 2px solid #26a4e3;
  padding: 5px 0 6px 10px;
  color: #888;
  font-size: 14px;
  outline: none;
  width: 100%;
}
input[type="submit"]{
  display: block;
  background-color: #26a4e3;
  color: #fff;
  cursor: pointer;
  border: none;
  min-width: 120px;
  padding: 10px 0;
}
</style>