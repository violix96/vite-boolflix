<script>
import { store } from '../store'
export default {
  name: 'SearchMovies',
  data(){
    return {
      store,
       inputText: '',
    }
  }
  
  

}
</script>

<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-danger">Cerca Film</h1>
        <div class="input-group mb-3">
          <input v-model="inputText" type="text" class="form-control" placeholder="Inserisci il nome del film o serie" @keyup.enter="$emit('search-event', inputText)" />
          <button @click="$emit('search-event', inputText)" class="btn btn-primary">Cerca</button>
        </div>
        <!-- Mostra i risultati MOVIE -->
        <div v-if="store.resultsMovie.length > 0" class="mt-5">
          <h2 class="text-center text-white">Risultati della ricerca Movie:</h2>
          <div class="row">
            <div v-for="film in store.resultsMovie" :key="film.id" class="col-md-4 mb-3">
              <div class="card" style="width: 18rem;">
                <img class="card-img-top">
                <div class="card-body">
                  <h5 class="card-title">{{ film.title }}</h5>
                  <h6 class="card-subtitle mb-2 text-muted">{{ film.original_title }}</h6>
                  <p class="card-text">Lingua: 
                    {{ film.original_language }}</p>
                  <p class="card-text">Voto: {{ film.vote_average }}</p>
                  <img class="flag" :src="'/public/img/' + film.original_language + '.svg'" alt="">
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- TV -->
        <div v-if="store.resultsTv.length > 0" class="mt-5">
          <h2 class="text-center text-white">Risultati della ricerca Tv:</h2>
          <div class="row">
            <div v-for="tv in store.resultsTv" :key="tv.id" class="col-md-4 mb-3">
              <div class="card" style="width: 18rem;">
                <img class="card-img-top">
                <div class="card-body">
                  <h5 class="card-title">{{ tv.name }}</h5>
                  <h6 class="card-subtitle mb-2 text-muted">{{ tv.original_name }}</h6>
                  <p class="card-text">Lingua: 
                    {{ tv.original_language }}</p>
                  <p class="card-text">Voto: {{ tv.vote_average }}</p>
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
  margin-top: 50px;

}

.flag{
  width: 50px;
}


</style>
  