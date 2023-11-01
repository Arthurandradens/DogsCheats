<template>
    <v-container>
      <v-row>
        <v-col
          v-for="name in characterNames"
        
          cols="12"
      
        >
          <v-card>
            <v-card-title>{{ name }}</v-card-title>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  export default {
    setup() {
      const characterNames = ref([]);
  
      const getUsers = async () => {
        try {
          const response = await axios.get('https://rickandmortyapi.com/api/character');
          for (let i = 0; i < 10; i++) {
            characterNames.value.push(response.data.results[i].name);
          }
        } catch (error) {
          console.error(error);
        }
      };
  
      onMounted(getUsers);
  
      return {
        characterNames,
      };
    },
  };
  </script>