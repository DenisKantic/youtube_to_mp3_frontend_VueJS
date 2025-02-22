<script setup></script>

<template>
  <v-container>
    <v-card style="width: 50%; margin: auto">
      <h1 class="text-center text-h5 py-5">
        <v-icon class="mr-2" size="30">mdi-music</v-icon>Download youtube video to mp3
      </h1>
      <v-text-field class="px-10" label="Paste link here" color="primary"></v-text-field>
      <v-divider thickness="3" color="primary"></v-divider>
      <v-card-actions class="mx-auto">
        <v-btn color="primary" variant="flat">Download</v-btn>
        <v-btn color="warning" variant="outlined">Refresh</v-btn>
      </v-card-actions>
      <v-divider thickness="3" color="primary"></v-divider>

      <v-card-subtitle class="text-center text-h5 py-5">Downloaded songs</v-card-subtitle>
      <v-infinite-scroll height="45vh" :items="items" :onLoad="load">
        <template v-for="(item, index) in items" :key="item">
          <div :class="['pa-2 text-h6', index % 2 === 0 ? 'bg-grey-lighten-2' : '']">
            Item number #{{ item }} <v-btn size="40" class="float-right"><v-icon size="20">mdi-download</v-icon></v-btn>
          </div>
        </template>
      </v-infinite-scroll>
    </v-card>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'

const items = ref(Array.from({ length: 30 }, (k, v) => v + 1))

async function api() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(Array.from({ length: 10 }, (k, v) => v + items.value.at(-1) + 1))
    }, 1000)
  })
}
async function load({ done }) {
  // Perform API call
  const res = await api()

  items.value.push(...res)

  done('ok')
}
</script>

<style scoped>
.v-container {
  width: 100%;
  min-height: 100vh;
  background-color: aliceblue;
}
@media screen and (max-width: 800px) {
  .v-card{
    width: 90% !important;
  }
}

</style>
