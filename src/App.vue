<template>
  <v-app>
    <v-main>
      <stereotech-brandbook />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import StereotechBrandbook from './StereotechBrandbook.vue';

@Component({
  components: {
    StereotechBrandbook,
  },
})
export default class App extends Vue { }
</script>

<style>
</style>
