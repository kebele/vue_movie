<template>
    <div class="movie-detail">
<!-- <h2>movie title</h2> -->
<h2>{{movie.Title}}</h2>
<p>{{ movie.Year}}</p>
<img :src="movie.Poster" alt="movie poster" class="featured-img">
<p>{{ movie.Plot }}</p>
    </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
import env from '@/env.js'

export default {
    setup() {
        const movie = ref({})
        const route = useRoute()

        onBeforeMount(() => {
            // console.log("before mount")
            fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
                .then(res => res.json())
                .then(data => {
                    console.log(data);
                    movie.value = data
                })
        });
        return {
            movie,
        }
    }
}
</script>

<style lang="scss">
    .movie-detail{
        padding: 16px;

        h2{
            color: whitesmoke;
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 16px;
        }

        .featured-img{
            display: block;
            max-width: 200px;
            margin-bottom: 16px;
        }

        p {
            color: whitesmoke;
            font-size: 17px;
            line-height: 1.4;
        }
    }
</style>