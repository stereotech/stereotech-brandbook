<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12" class="text-center">
        <h3 class="text-h2">Базовые цвета</h3>
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="accent" name="Цвет текста" />
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="primary" name="Акцент" />
      </v-col>

      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="additional" name="Дополнительный" />
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="background" name="Светлый фон" />
      </v-col>
      <v-col cols="12" class="text-center">
        <h3 class="text-h2">Цвета состояний</h3>
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="error" name="Ошибка" />
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="info" name="Информация" />
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="success" name="Успех" />
      </v-col>
      <v-col cols="12" sm="6" md="3">
        <ColorCard :color="warning" name="Предупреждение" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import ColorCard from './ColorCard.vue'
@Component({
  components: {
    ColorCard
  }
})
export default class ColorsTab extends Vue {
  primary: string = '#0277bd'
  accent: string = '#191b38'
  additional: string = '#adb4b9'
  background: string = '#ffffff'
  error: string = '#FF5252'
  info: string = '#9C27B0'
  success: string = '#4CAF50'
  warning: string = '#FFC107'
}
</script>

<style>
</style>