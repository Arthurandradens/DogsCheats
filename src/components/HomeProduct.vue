<template>
  <v-container>
    <h1>Dashboard</h1>
    <v-row justify="center">
      <v-col v-for="(character, id) in paginatedImages" :key="id" cols="12" sm="6" md="4" lg="2">
        <v-card flat class="border fill-height" style="display: flex; flex-direction: column; justify-content: space-between;">
          <v-img class="align-end text-white" :src="character.image" height="200px">
            <v-card-title> {{ character.name }}</v-card-title>
          </v-img>

          <v-card-subtitle class="pt-3">learn all about them</v-card-subtitle>

          <v-card-text>
            <div>Lorem ipsum dolor sit amet</div>
          </v-card-text>

          <v-card-actions>
            <v-btn variant="outlined" color="primary">See more</v-btn>
            <v-btn prepend-icon="mdi-cart" variant="tonal" color="error">Buy</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12">
        <div class="text-center">
          <v-pagination
            v-model="currentPage"
            :length="5"
            prev-icon="mdi-menu-left"
            next-icon="mdi-menu-right"
          ></v-pagination>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      Dogs: [],
      response: null,
      currentPage: 1,
      pageSize: 4
    };
  },
  computed: {
    paginatedImages() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.Dogs.slice(startIndex, endIndex);
    },
  },
  methods: {

    onPageChange(page){
      this.currentPage = page;
    },

    async getUsersImage() {
      // try {
      //   const apiKey = "live_kK6musSfztwmJAeZdoV7YFDPqHUHrw7fpByYIj10zCFPqbLlS5X9Br0viurLSlC7'";
      //   const url = 'https://api.thedogapi.com/v1/images/search?limit=10';

      //   axios
      //   .get(url,{
      //     headers:{
      //       'x-api-key': apiKey
      //     }
      //   })
      //   .then(response => {
      //     this.Dogs = response.data
          
      //   })
      // }
         
      try {
        this.response = await axios.get('https://rickandmortyapi.com/api/character');
        this.Dogs = this.response.data.results;
        
        } 
      catch (error) {
        console.error(error);
      }
    },
  },
  created() {
    this.getUsersImage();
  },
};
</script>
