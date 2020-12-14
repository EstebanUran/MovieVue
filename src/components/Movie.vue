<template>
  <div class="hello">
    <div class="container pt-5">
      <div class="row">
        <div class="col-8 ml-auto mr-auto">
          <div class="form-group">
            <label class="label">Buscar Pelicula</label>
            <input
              minlength="2"
              type="text"
              class="form-control"
              id="movieSearchTitle"
              placeholder="Enter the movie title, at least 2 characters"
              v-model="search"
            />
          </div>
          <div class="form-group w-100">
            <button
              type="submit"
              class="btn btn-info w-100"
              @click="fetchMovie"
            >
              Search
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="container pt-5" v-if="mostrar">
      <div class="row">
        <div class="card col-4 ml-auto mr-auto mb-5" style="width: 18rem">
          <img :src="movie.Poster" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title" v-text="movie.Title"></h5>
            <h5 class="card-title" v-text="movie.Year"></h5>
            <p class="card-text" v-text="movie.Plot"></p>
          </div>
          <ul class="list-group list-group-flush">
            <li class="list-group-item" v-text="movie.Production"></li>
            <li class="list-group-item" v-text="movie.Actors"></li>
            <li class="list-group-item" v-text="movie.Awards"></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Movie",
  data() {
    return {
      search: "",
      movie: {},
      mostrar: false,
    };
  },
  methods: {
    fetchMovie() {
      fetch("http://www.omdbapi.com/?apikey=23daade9&t=" + this.search)
        .then((data) => data.json())
        .then((response) => {
          if (response['Response'] == "True") {
          this.movie = response;
          this.mostrar = true;
          console.log(this.movie);
          }else{
             this.mostrar = false;
          }
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.label {
  font-size: 2em;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
