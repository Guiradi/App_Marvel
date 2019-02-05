<template>
  <div class="fade-in">
    <v-flex xs12>
      <img src="../assets/marvel-logo.png" alt="Logo da Marvel" width="100%">
    </v-flex>
    <app-personagens></app-personagens>
  </div>
</template>

<script>
// @ is an alias to /src
import Personagens from "@/components/Personagens.vue";

export default {
  components: {
    "app-personagens": Personagens
  }
};
</script>
