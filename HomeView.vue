<template>
  <main>
    <h2>Movies</h2>
    <div class="inputbut">
      <input v-model="search" type="search" placeholder="Search movie title" />
      <button @click="getPost">
        Search
      </button>
    </div>
    <div class="title">
      <ul class="movie-item" v-if="post.length"> 
        <li v-for="movie in post" 
        :key="movie.imdbID" 
        >
          <img v-if="movie.Poster !== 'N/A'" 
          :src="movie.Poster" alt="Movie Poster">
          <div>
            <h3>{{ movie.Title }}</h3>
            <p>Year: {{ movie.Year }}</p>
            <p>Plot: {{ movie.Plot }}</p>
           
          </div>
        </li>
      </ul>
      <p v-else class="item">No movies found.</p>
    </div>
    
  </main>
  
</template>

<script>
export default {
  data() {
    return {
      post: [],
      search: ''
    };
  },
  methods: {
    getPost() {
      fetch(`https://www.omdbapi.com/?s=${encodeURIComponent(this.search)}&apikey=315c77f4`)
        .then(response => response.json())
        .then(data => {
          if (data && data.Search) {
            this.post = data.Search;
          } else {
            this.post = [];
          }
        });
    }
  }
}
</script>

<style>
main {
  max-width: 1100px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h2 {
  text-align: center;
}

.inputbut {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px 0 0 5px;
  flex: 1;
}

button {
  padding: 8px 12px;
  background-color: #007BFF;
  color: #fff;
  border: none;
  border-radius: 5px 5px 5px 5px;
  cursor: pointer;
  margin-left: 10px;
}

ul {
  list-style: none;
  padding: 0;
}

li.movie-item {
  display: flex;
  margin-bottom: 20px;
}

img {
  width: 300px;
  height: 200px;
  object-fit: cover;
  margin-right: 20px;
  border-radius: 5px;
  
  

}

h3 {
  margin: 0;
  margin-bottom: 5px;
}

p {
  margin: 0;
  margin-bottom: 10px;
}

.title {
  color: crimson;
  
}

.movie-item {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

</style>

