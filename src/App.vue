<template>
  <v-app>
    <v-app-bar color="indigo" dark>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>Rick and Morty Characters</v-toolbar-title>
    </v-app-bar>
    <v-main>
      <v-container class="mt-10">
        <v-row >
          <v-col
            v-for="(character, index) in characters"
            :key="index"
            cols="12"
            md="4"
            class="my-5"
          >
            <v-card class="mx-auto"
    max-width="500">
              <v-img :src="character.image" aspect-ratio="1.0"></v-img>
              <v-card-title>{{ character.name }}</v-card-title>
              <v-card-subtitle>{{ character.status }}</v-card-subtitle>
              <v-card-text>
                <p>Species: {{ character.species }}</p>
                <p>Type: {{ character.type }}</p>
                <p>Gender: {{ character.gender }}</p>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const characters = ref([]);

    onMounted(async () => {
      const response = await axios.get('https://rickandmortyapi.com/api/character');
      characters.value = response.data.results;
    });

    return { characters };
  },
};
</script>
<style>
  .title {
    text-align: center;
    font-size: 36px;
    margin: 20px 0;
  }
  
  v-main {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }
</style>