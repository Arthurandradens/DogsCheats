<template>
    <div>
        <v-row>
            <v-col>
            <v-card-text>
                <v-text-field
                @keyup="highlightUser"
                :loading="loading"
                density="compact"
                variant="outlined"
                v-model="searchUser"
                label="Search"
                append-inner-icon="mdi-magnify"
                @click:append-inner="highlightUser"></v-text-field>
            </v-card-text>
            </v-col>
        </v-row>
    </div>
</template>


<script setup>
import { ref } from 'vue';

const searched = ref('');
const emit = defineEmits(['highlight-user'])

function highlightUser() {
    emit('highlight-user', searched.value)
}
</script>


<style>

</style>