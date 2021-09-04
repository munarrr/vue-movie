<template>
  <div class="movie-detail">
    <h2>{{movie.Title}}</h2>
    <p>{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />  
    <h3>Автор:  {{movie.Actors}}</h3>
    <h3>Цена:  {{movie.BoxOffice}}</h3>
    <h3>Язык: {{movie.Language}}</h3>
     <p>{{ movie.Plot }}</p>  
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';

export default {
  setup () {
    const movie = ref({});
    const route = useRoute();
    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=8930243d&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
          movie.value = data;
          console.log(data)
        });
    });
    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;
  text-align: center;
  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
    margin: 0 auto;
  }
  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;
    margin: 15px 0;
  }
  h3{
    margin: 10px 0;
  }
}
</style>