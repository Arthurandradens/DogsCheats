<template>
  <v-container>
    <v-card>
      <div class="d-flex justify-space-between">
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
                  <v-text-field 
                  clearable 
                  label="Status" 
                  variant="outlined"
                  :rules="validateName" ></v-text-field>
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
      </div>
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
          <tr v-for="(user, index) in character" :key="index" cols="12">
            <td>{{ user.name }}</td>
            <td>
              <v-chip size="small" variant="outlined" color="blue">
                <span style="color: #fff;">{{ user.status }}</span>
              </v-chip>
            </td>
           <td>
            <v-chip v-if="user.species === 'Human'" size="small" variant="outlined" color="blue" > 
              <span  style="color: white;">{{ user.species }}</span>
            </v-chip> 
            <v-chip v-if="user.species === 'Alien'" size="small" variant="outlined" color="green"> 
              <span  style="color: white;">{{ user.species }}</span>
            </v-chip> 
          </td>
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
import axios from 'axios';

export default {
  data() {
    return {
      character: [],
      response: null,
      isDialog: false,
      speciesArray: [],
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
  },
  created() {
    this.getUsers();
    
  }
};
</script>
