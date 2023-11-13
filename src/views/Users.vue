<template>
  <v-container>
    <v-card>
      <v-row>
        <v-col class="d-flex justify-space-between">
          <v-card-title>--Users List--</v-card-title>
          <v-btn @click="isDialog = true" class="mt-4 mr-4" variant="tonal" size="small"> New User </v-btn>
          <v-dialog v-model="isDialog" width="500px">
            <v-card>
              <v-card-text>Add User</v-card-text>
              <v-card-text>
                <v-row>
                  <v-col>
                    <v-text-field 
                    clearable 
                    label="Name" 
                    variant="outlined"
                    :rules="validateName"></v-text-field>
                  </v-col>
                  <v-col>
                    <v-select 
                    clearable 
                    label="Status" 
                    variant="outlined"
                    :rules="validateName"
                    :items="statusArray" ></v-select>
                  </v-col>               
                </v-row>

                <v-select
                  class="mt-3"
                  label="Species"
                  variant="outlined"
                  :items="speciesArray"
                >
                </v-select>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn variant="text" @click="isDialog = false" >Cancel</v-btn>
                <v-btn variant="tonal" color="success">Save</v-btn>
              </v-card-actions>

            </v-card>
          </v-dialog>
        </v-col>
      </v-row>
                                      <Search @highlight-user="highlightUser" />
      <v-table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Status</th>
            <th>Specie</th>
            <th>Actions</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(user, index) in character"
           :key="index" 
           cols="12">
            <td
            :class="{highlight:user.name.includes(highlight)}">{{ user.name }}</td>
            <td>
              <v-chip size="small" variant="outlined" :color="putStatusColor(user.status)">
                {{ user.status }}
              </v-chip>
            </td>
            <td>
              <v-chip size="small" variant="outlined" :color="putSpecieColor(user.species)">
                {{ user.species }}
              </v-chip>
            </td>
            <td>
              <v-btn variant="tonal" color="primary">Edit</v-btn>
              <v-btn class="ml-2" variant="tonal" @click="deleteUser(index)" color="error">Delete</v-btn>
            </td>
          </tr>
        </tbody>
      </v-table>
    </v-card>
  </v-container>
</template>

<script>
import axios from 'axios';
import Search from '@/layouts/Search.vue'
import { ref } from 'vue';
export default {
  components:{
    Search,
  },
  data() {
    return {
      character: [],
      response: null,
      isDialog: false,
      speciesArray: [],
      statusArray: [],
      namesArray: [],
      highlight: ref(''),
      searched: '',

      validateName: [
        value => {
          if (value) return true
            return "Campo obrigatório"
        }
      ],
      validateStatus: [
        value => {
          if (value) return true
            return "Campo obrigatório"
        }
      ]
    };
  },
  methods: {
    async getApi() {
      try {
        this.response = await axios.get('https://rickandmortyapi.com/api/character');
        return this.response.data.results;
      } catch (error) {
        console.error(error);
        return [];
      }
    },
    async getUsers() {
      try {
        const response = await this.getApi();
        this.character = response;
        await this.getUsersSpecies();
        await this.getUsersStatus();
        await this.getUsersName();
        return this.character;
      } catch (error) {
        console.error(error);
        return [];
      }
    },
    async getUsersSpecies() {
      this.character.forEach((character) => {
        // verifica se já existe uma especie
        // se não existir, ele inclue
       if(!this.speciesArray.includes(character.species)){
          this.speciesArray.push(character.species)
       } 
      });
    },
    async getUsersStatus() {
      this.character.forEach((character) => {
        // verifica se já existe um status
        // se não existir, ele inclue
       if(!this.statusArray.includes(character.status)){
          this.statusArray.push(character.status)
       } 
       
      });
    },

    async getUsersName() {
      this.character.forEach((character) => {
        // verifica se já existe um status
        // se não existir, ele inclue
       if(!this.namesArray.includes(character.name)){
          this.namesArray.push(character.name)
       } 
       
      });
    },
    putStatusColor(status){
      
      switch (status) {
        case 'Alive':
          return  'yellow-darken-4'
          break;
        case 'Dead':
          return  'red'
          break;
        case 'unknown':
          return  'blue-grey'
          break;
        default:
          break;
      }
    },
    putSpecieColor(specie){
      switch (specie) {
        case 'Human':
          return 'blue'
          break;
        case 'Alien':
          return 'green'
        default:
          break;
      }
    },
    highlightUser(searched){
      console.log('searched' + searched)
    }
  },
  created() {
    this.getUsers();
    
  }
};
</script>