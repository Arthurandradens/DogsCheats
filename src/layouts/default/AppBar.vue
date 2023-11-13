<template>
  <div>
    <v-navigation-drawer v-model="showMenu" app >
          <v-list>
            
            <v-list-item prepend-icon="mdi-home" @click="moveToHome()">Home</v-list-item>
    
            <v-list-item prepend-icon="mdi-account-group-outline" @click="moveToUsers()">Users</v-list-item>
            
            <v-list-item prepend-icon="mdi-pencil" @click="moveToComments()">Comments</v-list-item>
          </v-list>
    
    
        </v-navigation-drawer>
    <v-app-bar flat class="border-b" app>
          <v-app-bar-nav-icon @click="showMenu = !showMenu"></v-app-bar-nav-icon>
          <v-app-bar-title>Dogs cheats</v-app-bar-title>
          <v-btn dense icon="mdi-theme-light-dark" class="mr-2" @click="$vuetify.theme.dark = !$vuetify.theme.dark" ></v-btn>
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
      </div>
</template>

<script >
import router from "@/router";


  /**
   * Data
   */ 
  export default {
    data() {
      return {
         showMenu: false,

      }
    },
    methods: {
      moveToHome() {
       return router.push("/")
      },
      moveToUsers() {
        return router.push("/users")
      },
      moveToProfile(){
        return router.push("/profile")
      },
      moveToComments(){
        return router.push("/comments")
      },
    },
    created(){
      
    }
  }
  
</script>