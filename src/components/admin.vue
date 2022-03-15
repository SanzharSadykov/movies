<template>
    <div>
        <form class="block my-10" action="">
            <p class="text-xl font-bold">Enter title:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="text" v-model="form.title" placeholder="Enter title...">
            <p class="text-xl font-bold">Enter date:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="text" v-model="form.date" placeholder="Enter date...">
            <p class="text-xl font-bold">Enter description:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="text" v-model="form.desc" placeholder="Enter description...">
            <p class="text-xl font-bold">Enter image:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="text" v-model="form.image" placeholder="Enter image...">
            <p class="text-xl font-bold">Enter video:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="text" v-model="form.video" placeholder="Enter video...">
            <p class="text-xl font-bold">Enter metascore:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="number" v-model="form.meta" placeholder="Enter meta...">
            <p class="text-xl font-bold">Enter userscore:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="text" v-model="form.user" placeholder="Enter user...">
            <p class="text-xl font-bold">Enter genre:</p>
            <input class="block my-3 border-gray-500 w-full p-3 rounded-xl" type="text" v-model="form.genre" placeholder="Enter genre...">
            <button class="bg-green-400 px-20 py-4 text-white mx-auto block rounded-xl font-bold text-center" @click="addMovie()">
                Commit Movie
            </button>
        </form>
    </div>
</template>

<script> 
import axios from "axios"; 
 
export default { 
  data() { 
    return { 
      movies: [],
      baseURL: "http://localhost:3001/movies",
      form: {
          title: "",
          date: "",
          desc: "",
          image: "",
          video: "",
          meta: 0,
          user: "",
          genre: ""
      }
    }; 
  }, 
    async created() { 
    try { 
      const res = await axios.get(this.baseURL); 
      this.movies = res.data; 
    } catch (e) { 
      console.error(e); 
    } 
  }, 
  methods: {
    async addMovie() {
      try {
        const res = await axios.post(this.baseURL, {
            title: this.form.title,
            date: this.form.date,
            desc: this.form.desc,
            image: this.form.image,
            video: this.form.video,
            meta: this.form.meta,
            user: this.form.user,
            genre: this.form.genre            
        });
        this.movies = [...this.movies, res.data];
      } catch (e) {
        console.error(e);
      }
    }
  }
}; 
</script>
