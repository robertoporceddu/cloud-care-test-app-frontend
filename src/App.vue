<template>
  <v-app>
    <v-main>
      <BeerPage/>
    </v-main>
  </v-app>
</template>

<script>
import BeerPage from './pages/Beer.vue';

export default {
  name: 'App',

  components: {
    BeerPage
},

  data: () => ({
    //
  }),
}
</script>
