<template>
  <v-navigation-drawer v-model="showMenu" >
        <v-list>
          
          <v-list-item prepend-icon="mdi-home" @click="moveToHome()">Home</v-list-item>
  
          <v-list-item prepend-icon="mdi-account-group-outline" @click="moveToUsers()">Users</v-list-item>
          
  
          <v-list-group value="Clients">
            <template #activator="{ props }">
  
  
                <v-list-item
                v-bind="props"
                prepend-icon="mdi-account-circle"
                title="Clients"
                >
  
                </v-list-item>
              
            </template>
  
          <v-list-item  prepend-icon="mdi-account-box-multiple">
            All
          </v-list-item>
  
          <v-list-item prepend-icon="mdi-account-eye">
            Active clients
          </v-list-item>
  
          </v-list-group>
  
  
        </v-list>
  
  
      </v-navigation-drawer>
  <v-app-bar flat class="border-b">
        <v-app-bar-nav-icon @click="showMenu = !showMenu"></v-app-bar-nav-icon>
        <v-app-bar-title>Dogs cheats</v-app-bar-title>
        <template #append >
          <v-menu>
            <template #activator="{ props }">
              
              <v-avatar v-bind="props">
                <v-img 
                cover 
                src="@/assets/gato.jpeg">
  
                </v-img>
              </v-avatar> 
  
            </template>
            
            <v-card min-width="200px" >
  
              <v-list density="compact" nav>
                <v-list-item @click="moveToProfile()" prepend-icon="mdi-account-outline">
                  <v-list-title >My profile</v-list-title>
                </v-list-item>
  
                <v-list-item prepend-icon="mdi-star">
                  <v-list-title>My favorites</v-list-title>
                </v-list-item>
  
              </v-list>
            </v-card>     
          </v-menu>
        </template>
  
      </v-app-bar>
</template>

<script setup>
import router from "@/router";
import { ref } from "vue";

  /**
   * Data
   */
  const showMenu = ref(true);

  /**
   * methods
   */

  const moveToHome = () => {
    router.push("/")
  };
  const moveToUsers = () => {
    router.push("/users")
  };
  const moveToProfile = () => {
    router.push("/profile")
  }

</script>