<template>
  <v-container>
    <v-row justify="center" align="center">
      <template v-for="(item, index) in items">
        <v-col
          cols="12"
          class="text-center"
          v-if="typeof item === 'string'"
          :key="index"
        >
          <h3 class="text-h2">{{ item }}</h3>
        </v-col>
        <v-col cols="12" sm="6" md="4" v-else :key="index">
          <LogoCard :path="item.path" :title="item.title" :dark="item.dark" />
        </v-col>
      </template>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import LogoCard from './LogoCard.vue'
@Component({
  components: {
    LogoCard
  }
})
export default class LogosTab extends Vue {
  items: Array<{ path: string, title: string, dark?: boolean } | string> = [
    'Основной логотип',
    {
      path: 'logo/base_logo/base',
      title: 'Базовый логотип'
    },
    {
      path: 'logo/round_logo/round',
      title: 'Логотип'
    },
    //{
    //  path: 'logo/vert_logo/vert',
    //  title: 'Вертикальный вариант'
    //},
    //{
    //  path: 'logo/text_logo/text',
    //  title: 'Только текст'
    //},
    {
      path: 'logo/tm_logo/tm',
      title: 'Товарный знак'
    },
    'Для темного фона',
    {
      path: 'logo/base_logo_dark/base',
      title: 'Базовый логотип',
      dark: true
    },
    {
      path: 'logo/round_logo_dark/round',
      title: 'Логотип',
      dark: true
    },
    //{
    //  path: 'logo/vert_logo_dark/vert',
    //  title: 'Вертикальный вариант',
    //  dark: true
    //},
    //{
    //  path: 'logo/text_logo_dark/text',
    //  title: 'Только текст',
    //  dark: true
    //},
    {
      path: 'logo/tm_logo_dark/tm',
      title: 'ТОварный знак',
      dark: true
    },
    'Логотипы приложений',
    {
      path: 'logo/steapp_logo/steapp',
      title: 'STE App'
    },
    {
      path: 'logo/steslicer_logo/steslicer',
      title: 'STE Slicer'
    },
    {
      path: 'logo/stereotechcloud_logo/stereotechcloud',
      title: 'Stereotech Cloud'
    }
  ]
}
</script>

<style>
</style>