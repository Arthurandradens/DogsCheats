<template>
    <v-container>
    <v-card>
      <div class="d-flex justify-space-between">
        <v-card-title>--Users List--</v-card-title>
        <v-dialog width="500px">
          <template #activator="{ props }"> 
            <v-btn v-bind="props" class="mt-4 mr-4" variant="tonal" size="small"> New User </v-btn>
          </template>
          <v-card>
            <v-card-title>teste</v-card-title>
          </v-card>
        </v-dialog>
      </div>
      <v-table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Status</th>
            <th>Actions</th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="(user,index) in characterNames"
            :key="index"
             cols="12">
            <td>{{ user.name }}</td>
            <td> {{ user.status }} </td>
            <td>
              <v-btn variant="tonal" color="primary">Edit</v-btn>
              <v-btn class="ml-2" variant="tonal" color="error">Delete</v-btn>
            </td>
          </tr>
        </tbody>
      </v-table>
    </v-card>
    </v-container>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  export default {
    // setup() {
    //   const characterNames = ref([]);

    //   const getUsers = async () => {
    //     try {
    //       const response = await axios.get('https://rickandmortyapi.com/api/character');
    //       for (let i = 0; i < 10; i++) {
    //         characterNames.value.push(response.data.results[i]);
    //       }
    //     } catch (error) {
    //       console.error(error);
    //     }
    //   };
  
    //   onMounted(getUsers);
  
    //   return {
    //     characterNames,
    //   };
    // },
    data(){
      return{
         characterNames: [],
         response: null
      }
    },
    methods: {
     async getUsers(){
        try{
          this.response = await axios.get('https://rickandmortyapi.com/api/character');
          for(let i = 0; i < 10; i++){
            this.characterNames.push(this.response.data.results[i]);
        }
      }
      catch(error){
            console.error(error)
          }
    }
  },

  created(){
    this.getUsers()
  }
}
  </script>