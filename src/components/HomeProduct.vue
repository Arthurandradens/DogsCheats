<template>
  <v-container>
          <h1>Dashboard</h1>
  
          <v-row>
            <v-col cols="12" sm="6" md="4" lg="3">
              <v-card flat class="border fill-height">
                <v-img
                  class="align-end text-white"
                  src="@/assets/golden.jpg"
                  height="200px"
                >
                  <v-card-title>Golden puppy</v-card-title>
                </v-img>
  
                <v-card-subtitle class="pt-3">learn all about them</v-card-subtitle>
  
                <v-card-text>
                  <div>Lorem ipsum dolor sit amet</div>
                </v-card-text>
  
                <v-card-actions>
                  <v-btn variant="outlined" color="primary" >See more</v-btn>
                  <v-btn prepend-icon="mdi-cart" variant="tonal" color="error">Buy</v-btn>
                  <!-- <v-btn @click="toggleStar(0)" :icon="items[0].star" variant="" color="error"></v-btn> -->
                </v-card-actions>
              </v-card>
            </v-col>
  
            <v-col cols="12" sm="6" md="4" lg="3">
              <v-card flat class="border fill-height">
                <v-img
                  class="align-end text-white"
                  src="@/assets/golden.jpg"
                  height="200px"
                >
                  <v-card-title>Golden puppy</v-card-title>
                </v-img>
  
                <v-card-subtitle class="pt-3">learn all about them</v-card-subtitle>
  
                <v-card-text>
                  <div>Lorem ipsum dolor sit amet</div>
                </v-card-text>
  
                <v-card-actions>
                  <v-btn variant="outlined" color="primary" >See more</v-btn>
                  <v-btn prepend-icon="mdi-cart" variant="tonal" color="error">Buy</v-btn>
                  <!-- <v-btn @click="toggleStar(1)" :icon="items[1].star" variant="" color="error"></v-btn> -->
                </v-card-actions>
              </v-card>
            </v-col>
  
            <v-col cols="12" sm="6" md="4" lg="3">
              <v-card flat class="border fill-height">
                <v-img
                  class="align-end text-white"
                  src="@/assets/golden.jpg"
                  height="200px"
                >
                  <v-card-title>Golden puppy</v-card-title>
                </v-img>
  
                <v-card-subtitle class="pt-3">learn all about them</v-card-subtitle>
  
                <v-card-text>
                  <div>Lorem ipsum dolor sit amet</div>
                </v-card-text>
  
                <v-card-actions>
                  <v-btn variant="outlined" color="primary" >See more</v-btn>
                  <v-btn prepend-icon="mdi-cart" variant="tonal" color="error">Buy</v-btn>
                  <!-- <v-btn @click="toggleStar(2)" :icon="items[2].star" variant="" color="error"></v-btn> -->
                </v-card-actions>
              </v-card>
            </v-col>
  
            <v-col cols="12" sm="6" md="4" lg="3">
              <v-card flat class="border fill-height">
                <v-img
                  class="align-end text-white"
                  src="@/assets/golden.jpg"
                  height="200px"
                >
                  <v-card-title>Golden puppy</v-card-title>
                </v-img>
  
                <v-card-subtitle class="pt-3">learn all about them</v-card-subtitle>
  
                <v-card-text>
                  <div>Lorem ipsum dolor sit amet</div>
                </v-card-text>
  
                <v-card-actions>
                  <v-btn variant="outlined" color="primary" >See more</v-btn>
                  <v-btn prepend-icon="mdi-cart" variant="tonal" color="error">Buy</v-btn>
                  <!-- <v-btn @click="toggleStar(3)" :icon="items[3].star" variant="" color="error"></v-btn> -->
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
</template>

<script setup>
import router from '@/router';
import axios from "axios";
import { ref } from 'vue';

/**
 * Data
 */
const nome = ref(null);
  
  /**
   * Methods
   */
  // const navegar = () => {
  //   router.push('/page-two')
  // }

  // const axios = require('axios');
  const chamaAPI = () => {
    axios.get('https://rickandmortyapi.com/api/character')
    .then((response) => {
      for(let i = 0; i < 10 ; i++){
        console.log(response.data.results[i].name);
      }
    })
    .catch((error) => {
      console.log(error.data)
    })
    .finally()
  };
</script>