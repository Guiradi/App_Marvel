<template>
  <div v-if="!loading">
    <v-layout column align-start class="listaPersonagens">
      <v-container fluid grid-list-md>
        <v-layout row wrap>
          <v-flex xs12 md6 lg2 v-for="personagem in personagens" :key="personagem.id">
            <v-card height="300px">
              <a href="#">
                <v-img id="img-personagem" :src="getImagem(personagem)" height="200px"></v-img>
              </a>
              <v-card-text primary-title>
                <span class="name text-xs-center">{{ personagem.name }}</span>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-layout>
  </div>
</template>

<script>
// Imports:
import axios from "axios";
import md5 from "md5";

export default {
  data() {
    return {
      personagens: null,
      loading: false
    };
  },
  created() {
    this.fetchData();
  },
  watch: {
    $route: "fetchData"
  },
  methods: {
    fetchData() {
      this.personagens = null;
      this.loading = true;

      // Variáveis para a URL de requisição:
      const urlBase = "https://gateway.marvel.com/v1/public/characters?apikey=";
      const publicKey = "0d3447d34a37b0e74273f537b77a29a7";
      const urlPersonagens = urlBase + publicKey + "&limit=18";
      console.log("URL de Requisição -> ", urlPersonagens);
      axios
        .get(urlPersonagens)
        .then(response => {
          this.loading = false;
          this.personagens = response.data.data.results;
        })
        .catch();
    },
    getImagem: function(personagem) {
      if (personagem.thumbnail.path != null) {
        return personagem.thumbnail.path + "/portrait_large.jpg";
      }
    }
  }
};
</script>

<style scoped>
#img-personagem {
  margin-top: 10px;
}

.name {
  font-size: 28px;
  font-family: Marvel;
}
</style>
