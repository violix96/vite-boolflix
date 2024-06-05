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
      <div class="col-md-6 offset-md-3">
        <h1 class="text-center text-danger">Cerca Film</h1>
        <div class="input-group mb-3">
          <input v-model="inputText" type="text" class="form-control" placeholder="Inserisci il nome del film o serie" @keyup.enter="$emit('search-event', inputText)" />
          <button @click="$emit('search-event', inputText)" class="btn btn-primary">Cerca</button>
        </div>
        <!-- Mostra i risultati -->
        <div v-if="store.results.length > 0" class="mt-3">
          <h2 class="text-center text-white">Risultati della ricerca:</h2>
          <div v-for="film in store.results" :key="film.id" class="card mb-3">
           <div class="card-body">
            <h5 class="card-title">{{ film.title }}</h5>
            <h6 class="card-subtitle mb-2 text-muted">{{ film.original_title }}</h6>
            <p class="card-text">Lingua: {{ film.original_language }}</p>
              <p class="card-text">Voto: {{ film.vote_average }}</p>
           </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
  
  
<style>
.container {
  margin-top: 50px;
}
</style>
  