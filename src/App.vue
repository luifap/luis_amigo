<template>
  <div id="app">
    
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        
          <Tabla/>
          <BootstrapVueDatatable/>             
      </div>
    </div>

    
          

  <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        
          <h1 class="title">
            <span class="has-text-success">Personajes</span>
          </h1>   
          <div class="field has-addons is-pulled-right">

          <div class="control">
            <input 
            v-model = "search" 
            type="text" 
            placeholder = "Buscar por nombre"
            class="input is-rounded" 
            v-on:keyup.enter = "searchData">
          </div>

          <div class="control">
             <button 
             class="button is-success is-rounded"
              @click = "searchCharacter();">
              Buscar
            </button>
          </div>
        </div>         
      </div>
    </div>

          

        

    <div class="container">
        <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
          
          <character 
          @showModal = "showModal"
          :character = "character"
          v-for = "character of characters"
          :key= "character.id" 
          
          />
        </div>

        <nav class="pagination" role="navegation" aria-label="pagination">
          <a class="pagination-previous" v-on:click = "changePage(page - 1);">Anterior</a>

          <ul class="pagination-list">
            <li>
              <a class="pagination-link is-current">{{ page }}</a>
            </li>
          </ul>
          <a class="pagination-next" v-on:click = "changePage(page + 1);">Siguiente</a>
        </nav>
    </div>

    <div class="modal" 
          :class="{ 'is-active': modal }"
          v-if = "modal">

      <div class="modal-background"  @click= "modal = false;"></div>

      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-tittle">Acerca de: {{currentCharacter.name}} </p>
        </header>

        <div class="modal-card-body">
          <p>Genero:</p>
          <strong>{{ currentCharacter.gender }}</strong>

          <p>Estatus:</p>
          <strong>{{ currentCharacter.status }}</strong>

          <p>Especie:</p>
          <strong>{{ currentCharacter.species}}</strong>

          <p>Tipo:</p>
          <strong>{{ currentCharacter.type }}</strong>
        </div>
        

        <footer class="modal-card-food">
          <button class="button" @click= "modal = false;">Cerrar</button>
        </footer>

      </div>
      
    </div>
  </div>
</template>

<script>
// Importación de librerías
import axios from "axios";
import Character from "./components/Character";
import Tabla from "./components/Tabla.vue";
import BootstrapVueDatatable from "./components/BootstrapVueDatatable";


export default {
  name: "App",
  components: {
    Character,
    Tabla,
    BootstrapVueDatatable,
  },
 

  data: function() {
    return {
      characters: [],
      page: 1,
      pages: 1,
      search: "",
      modal: false,
      currentCharacter: {}
    };
    
  },
  created() {
    this.fetch();
  },
  methods: {
    async fetch() {
      const params = {
        page: this.page,
        name: this.search
      };

      let response = await axios.get(
        "https://rickandmortyapi.com/api/character/",
         { params }
        );

        this.pages = response.data.info.pages;
        this.characters = response.data.results;

        console.log(response.data.results);
      },
        
    changePage(page) {
      this.page = page <= 0 || page > this.pages ? this.page : page;
      this.fetch();
      window.scrollTo(0, 0);
    },
    searchCharacter() {
      this.page = 1;
      this.fetch();
    },
    showModal (id) {
      this.fetchOne(id);
    },
    async fetchOne(id) {

      let result = await axios.get(
        `https://rickandmortyapi.com/api/character/${id}`
      );
      this.currentCharacter = result.data;
      this.modal = true;

      console.log(this.currentCharacter, "Personajes");
    }
  }
};
</script>

