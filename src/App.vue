<template>
  <v-app>
    <v-main>
      <HerGacha/>
    </v-main>
  </v-app>
</template>

<script>
import HerGacha from './components/HerGacha.vue'

export default {
  name: 'App',

  components: {
    HerGacha,
  },

  data: () => ({
    //
  }),
}
</script>
