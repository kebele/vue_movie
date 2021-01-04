<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <!-- <img
          src="https://m.media-amazon.com/images/M/MV5BZmQ5NGFiNWEtMmMyMC00MDdiLTg4YjktOGY5Yzc2MDUxMTE1XkEyXkFqcGdeQXVyNTA4NzY1MzY@._V1_SX300.jpg"
          alt="Naruto Poster"
          class="featured-img"
        /> -->
        <img
          src="../assets/pexels-louis-1200450.jpg"
          alt="Naruto Poster"
          class="featured-img"
        />
        <div class="detail">
          <!-- <h3>naruto</h3>
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Asperiores
            molestias et illo, assumenda vel provident error voluptate totam
            facilis, quam expedita perferendis. Facere ratione aliquid hic
            distinctio consequatur eius expedita.
          </p> -->
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="search" v-model="search">
      <input type="submit" value="search">
    </form>

    <div class="movie-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <!-- {{ movie.Title }} -->
        <router-link :to="'/movie/'+movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="movie poster">
            <div class="type">{{ movie.Type}}</div>
          </div>
          <div class="detail">
            <p class="year">{{movie.Year}}</p>
            <h3>{{movie.Title}}</h3>
          </div>
        </router-link>
      </div>
    </div>
    <p class="footer"><a href="https://www.youtube.com/channel/UCBBGM84ZOs7z5jpTQAaZ_Hg">thanks to Tyler Potts for this app!</a></p>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref } from 'vue'
import env from '@/env.js'


export default {
  setup() {
    const search = ref("")
    const movies =  ref([])

    const SearchMovies = () => {
      if(search.value != ""){
        // console.log(search.value);
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(res => res.json())
          .then(data => {
            // console.log(data)
            movies.value = data.Search
            search.value = ""
            // console.log(movies.value);
          })
      }
    }


    return {
      search,
      movies,
      SearchMovies,
    }
  }
};
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;

      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      h3 {
        color: whitesmoke;
        margin-bottom: 16px;
      }

      p {
        color: whitesmoke;
      }
    }
  }
  .search-box{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input{
      display: block;
      appearance: none;
      bottom: none;
      outline: none;
      background: none;

      &[type="text"]{
        width: 100%;
        color: black;
        background-color: lightblue;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition : 0.4s;

        &::placeholder {
          color: gray;
        }

        &:focus{
          box-shadow: 0 0 6px 6px rgba(0,0,0,0.5);
        }
      }

      &[type="submit"]{
        width: 100%;
        max-width: 300px;
        background-color: steelblue;
        padding: 16px;
        border-radius: 8px;
        color: whitesmoke;
        font-size: 20px;
        text-transform: uppercase;
        transition : 0.4s;

        &:active {
          background-color: lightblue;
        }
      }
    }
  }
  .movie-list{
    display: flex;
    flex-wrap: wrap;
    margin: 0 8px;

    .movie{
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link{
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image{
          position: relative;
          display: block;

          img{
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type{
            position: absolute;
            padding: 8px 16px;
            background-color: steelblue;
            color: whitesmoke;
            bottom: 16px;
            left: 0;
            text-transform: capitalize;
          }
        }
        .detail {
          background-color: brown;
          padding: 16px 8px;
          flex : 1 1 100%;
          border-radius: 0 0 8px 8px;

          .year{
            color: whitesmoke;
            font-size: 14px;
          }
          h3 {
            color: whitesmoke;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}

.footer{
  position : fixed;
  bottom: 5%;
  right: 5%;
  font-size: 16px;
  background-color: gainsboro;
}
</style>
