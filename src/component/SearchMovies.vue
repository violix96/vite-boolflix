<script>
import { store } from '../store'
export default {
  name: 'SearchMovies',
  data() {
    return {
      store,
      inputText: '',
    }
  },
  methods: {
    convertVote(voto) {
      // console.log(Math.round(voto / 2))
      return Math.round(voto / 2);
    }
  }



}
</script>

<template>
  <header class="bg-black d-flex">
    <div class="container d-flex justify-content-between">
      <h1 class="text-danger">Boolflix</h1>
      <div class="input-group  cerca mt-2 mb-3">
        <input v-model="inputText" type="text" class="form-control" placeholder="Inserisci il nome del film o serie"
          @keyup.enter="$emit('search-event', inputText)" />
        <button @click="$emit('search-event', inputText)" class="btn btn-primary">Cerca</button>
      </div>
    </div>
  </header>
  <div class="container mt-2">
    <div class="row">
      <div class="col-4"></div>
      <div class="col-12">
        <!-- Mostra i risultati MOVIE -->
        <div v-if="store.resultsMovie.length > 0" class="mt-5">
          <h2 class="text-left my-5">Risultati della ricerca Movie:</h2>
          <div class="row">
            <div v-for="film in  store.resultsMovie " :key="film.id" class="col-md-4 mb-3">
              <div class="card" style="width: 18rem;">
                <img :src="'https://image.tmdb.org/t/p/w342/' + film.poster_path" class="card-img-top">
                <div class="card-body">
                  <h5 class="card-title">{{ film.title }}</h5>
                  <h6 class="card-subtitle mb-2 text-muted">{{ film.original_title }}</h6>
                  <p class="card-text">Lingua:
                    {{ film.original_language }}</p>
                  <p class="card-text">Voto:
                    <i v-for="star in convertVote(film.vote_average)" class="fas fa-star"></i>
                    <i v-for="star in 5 - convertVote(film.vote_average)" class="fa-regular fa-star"></i>
                  </p>
                  <img class="flag" :src="'/public/img/' + film.original_language + '.svg'" alt="">
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- TV -->
        <div v-if="store.resultsTv.length > 0" class="mt-5">
          <h2 class="text-left my-5">Risultati delle serie TV:</h2>
          <div class="row">
            <div v-for=" tv  in  store.resultsTv " :key="tv.id" class="col-md-4 mb-3">
              <div class="card" style="width: 18rem;">
                <img :src="'https://image.tmdb.org/t/p/w342/' + tv.poster_path" class="card-img-top">
                <div class="card-body">
                  <h5 class="card-title">{{ tv.name }}</h5>
                  <h6 class="card-subtitle mb-2 text-muted">{{ tv.original_name }}</h6>
                  <p class="card-text">Lingua:
                    {{ tv.original_language }}</p>
                  <p class="card-text">Voto:
                    <i v-for="star in convertVote(tv.vote_average)" class="fas fa-star"></i>
                    <i v-for="star in 5 - convertVote(tv.vote_average)" class="fa-regular fa-star"></i>
                  </p>
                  <img class="flag" :src="'/public/img/' + tv.original_language + '.svg'" alt="">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

  
  
<style scoped>
.container {
  margin-top: 10px;

}

.flag {
  width: 50px;
}

h2 {
  color: #DC3542;
}

.cerca {
  width: 400px;
}
</style>
  