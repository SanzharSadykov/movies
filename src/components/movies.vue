<template>
    <div class="container mx-auto">
        <div class="py-8 border-b border-gray-500" v-for="movie of movies" :key="movie.id">
            <div @click="$router.push({name: 'movie', params: {id: movie.id}})" class="flex justify-between items-start">
                <img :src="movie.image" alt="">
                <div class="pl-6 info w-3/4">
                    <h1 class="font-bold text-xl">{{ movie.id }}. {{ movie.title }}</h1>
                    <p class="my-2 text-gray-500">{{ movie.date }}</p>
                    <p>{{ movie.desc }}</p>
                    <div class="rating flex justify-start items-start">
                        <div class="block pr-6">
                            <p class="my-2 font-bold">Metascore:</p>
                            <p class="w-3/4 text-center bg-yellow-500 font-bold text-xl p-3 rounded-xl text-white">{{ movie.meta }}</p>
                        </div>
                        <div class="block">
                            <p class="my-2 font-bold">Userscore:</p>
                            <p class="w-3/4 text-center bg-green-500 font-bold text-xl p-3 rounded-full text-white">{{ movie.user }}</p>
                        </div>                       
                    </div>                   
                </div>
                <div class="items-center trailer pl-6">
                    <video muted autoplay controls width="500" height="240" :src="movie.video"></video>
                </div>
            </div>
        </div>
    </div>
</template>

<script> 
import axios from "axios"; 
 
export default { 
  data() { 
    return { 
      movies: [],
      baseURL: "http://localhost:3001/movies",
    }; 
  }, 
  async created() { 
    try { 
      const res = await axios.get(this.baseURL); 
      this.movies = res.data; 
    } catch (e) { 
      console.error(e); 
    } 
  }
}; 
</script>
