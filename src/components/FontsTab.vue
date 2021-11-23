<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="12" md="4">
        <v-btn
          text
          block
          color="primary"
          large
          href="https://fonts.google.com/download?family=Roboto"
        >
          <v-icon>mdi-download</v-icon>Загрузить шрифт
        </v-btn>
      </v-col>
      <v-col cols="12">
        <v-item-group mandatory>
          <v-sheet tile>
            <v-item
              v-for="[c, text, size, weight, spacing, margin] in classes"
              :key="c"
            >
              <template v-slot="{ active, toggle }">
                <v-sheet
                  :color="active ? 'grey lighten-4' : undefined"
                  class="px-4 pt-4 pb-3"
                  tile
                  style="cursor: pointer"
                  @click="toggle"
                >
                  <div
                    :class="[`text-${c}`, active && `mb-${margin}`]"
                    class="transition-swing"
                    v-text="text"
                  ></div>

                  <v-expand-transition>
                    <v-responsive v-if="active" max-width="350">
                      <div class="d-flex justify-space-between caption">
                        <div>
                          <div class="grey--text mb-2">Шрифт</div>

                          <div class="font-weight-medium">Roboto</div>
                        </div>

                        <div>
                          <div class="grey--text mb-2">Толщина</div>

                          <div class="font-weight-medium" v-text="weight"></div>
                        </div>

                        <div>
                          <div class="grey--text mb-2">Размер</div>

                          <div class="font-weight-medium" v-text="size"></div>
                        </div>

                        <div>
                          <div class="grey--text text-darken-1 mb-2">
                            Межбуквенное расстояние
                          </div>

                          <div
                            class="font-weight-medium"
                            v-text="spacing"
                          ></div>
                        </div>
                      </div>
                    </v-responsive>
                  </v-expand-transition>
                </v-sheet>
              </template>
            </v-item>
          </v-sheet>
        </v-item-group>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
@Component
export default class FontsTab extends Vue {
  classes = [
    ['h1', 'Заголовок 1', '6rem', '300', '-0.09375rem', -1],
    ['h2', 'Заголовок 2', '3.75rem', '300', '-0.03125rem', 0],
    ['h3', 'Заголовок 3', '3rem', '400', 'normal', 1],
    ['h4', 'Заголовок 4', '2.125rem', '400', '0.015625rem', 2],
    ['h5', 'Заголовок 5', '1.5rem', '400', 'normal', 2],
    ['h6', 'Заголовок 6', '1.25rem', '500', '0.009375rem', 3],
    ['subtitle-1', 'Подзаголовок 1', '1rem', '400', '0.009375rem', 4],
    ['subtitle-2', 'Подзаголовок 2', '0.875rem', '500', '0.00625rem', 4],
    ['body-1', 'Основной текст 1', '1rem', '400', '0.03125rem', 4],
    ['body-2', 'Основной текст 2', '0.875rem', '400', '0.015625rem', 4],
    ['button', 'Кнопка', '0.875rem', '500', '0.078125rem', 4],
    ['caption', 'Подпись', '0.75rem', '400', '0.025rem', 4],
    ['overline', 'Дополнительно', '0.75rem', '500', '0.1666666667em', 4],
  ]
}
</script>

<style>
</style>