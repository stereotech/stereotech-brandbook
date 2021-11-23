<template>
  <v-tabs
    centered
    center-active
    dark
    background-color="primary"
    icons-and-text
    v-model="tab"
  >
    <v-tab v-for="(item, index) in items" :key="index" :href="`#tab-${index}`">
      {{ item.name }}
      <v-icon>{{ item.icon }}</v-icon>
    </v-tab>
    <v-tabs-items touchless v-model="tab">
      <template v-for="(item, index) in items">
        <v-tab-item :value="`tab-${index}`" :key="`tab-${index}`">
          <component :is="item.component" />
        </v-tab-item>
      </template>
    </v-tabs-items>
  </v-tabs>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
import LogosTab from './components/LogosTab.vue'
import ColorsTab from './components/ColorsTab.vue'
import FontsTab from './components/FontsTab.vue'

@Component({
  components: {
    LogosTab,
    FontsTab,
    ColorsTab
  }
})
export default class StereotechBrandbook extends Vue {
  tab: any = null
  items: Array<{
    name: string,
    icon: string,
    component: string
  }> = [
      {
        name: 'Логотип',
        component: 'logos-tab',
        icon: 'mdi-checkbox-blank-circle-outline'
      },
      {
        name: 'Цвета',
        component: 'colors-tab',
        icon: 'mdi-palette'
      },
      {
        name: 'Шрифты',
        component: 'fonts-tab',
        icon: 'mdi-format-font'
      },
    ]
}

</script>

<style>
</style>