<template>
  <v-card :dark="dark" :color="dark ? 'accent' : 'secondary'">
    <v-card-title>{{ title }}</v-card-title>
    <v-card-text>
      <v-container>
        <v-row justify="center" align="center">
          <v-col cols="12">
            <v-img :src="`${path}.svg`" height="200" contain></v-img>
          </v-col>
          <v-col cols="12">
            <v-list outlined rounded>
              <v-subheader>Векторный</v-subheader>
              <v-list-item :href="`${path}.cdr`" download>
                <v-list-item-icon>
                  <v-icon>mdi-draw</v-icon>
                </v-list-item-icon>
                <v-list-item-title>CDR (CorelDraw 2019)</v-list-item-title>
              </v-list-item>
              <v-list-item :href="`${path}.svg`" download>
                <v-list-item-icon>
                  <v-icon>mdi-svg</v-icon>
                </v-list-item-icon>
                <v-list-item-title>SVG</v-list-item-title>
              </v-list-item>
              <v-subheader>Растровый</v-subheader>
              <v-list-item>
                <v-bottom-sheet>
                  <template v-slot:activator="{ on, attrs }">
                    <v-list-item v-on="on" v-bind="attrs">
                      <v-list-item-title>JPG</v-list-item-title>
                    </v-list-item>
                  </template>
                  <v-list>
                    <v-list-item
                      v-for="(item, index) in resolutions"
                      :key="index"
                      @click="getImage('jpg', item.value)"
                    >
                      <v-list-item-icon>
                        <v-icon>mdi-download</v-icon>
                      </v-list-item-icon>
                      <v-list-item-title>{{ item.text }}</v-list-item-title>
                    </v-list-item>
                    <v-list-item>
                      <v-container fluid>
                        <v-row>
                          <v-col cols="12" class="text-center">
                            <v-subheader class="pl-0">Высота в пкс</v-subheader>
                            <v-slider
                              max="4096"
                              min="16"
                              thumb-label
                              v-model="ownvalue"
                            ></v-slider>
                            <v-btn
                              text
                              outlined
                              color="primary"
                              @click="getImage('jpg', ownvalue)"
                            >
                              <v-icon>mdi-download</v-icon>Загрузить
                            </v-btn>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-list-item>
                  </v-list>
                </v-bottom-sheet>
              </v-list-item>
              <v-list-item>
                <v-bottom-sheet>
                  <template v-slot:activator="{ on, attrs }">
                    <v-list-item v-on="on" v-bind="attrs">
                      <v-list-item-title>PNG</v-list-item-title>
                    </v-list-item>
                  </template>
                  <v-list>
                    <v-list-item
                      v-for="(item, index) in resolutions"
                      :key="index"
                      @click="getImage('png', item.value)"
                    >
                      <v-list-item-icon>
                        <v-icon>mdi-download</v-icon>
                      </v-list-item-icon>
                      <v-list-item-title>{{ item.text }}</v-list-item-title>
                    </v-list-item>
                    <v-list-item>
                      <v-container fluid>
                        <v-row>
                          <v-col cols="12" class="text-center">
                            <v-subheader class="pl-0">Высота в пкс</v-subheader>
                            <v-slider
                              max="4096"
                              min="16"
                              thumb-label
                              v-model="ownvalue"
                            ></v-slider>
                            <v-btn
                              text
                              outlined
                              color="primary"
                              @click="getImage('png', ownvalue)"
                            >
                              <v-icon>mdi-download</v-icon>Загрузить
                            </v-btn>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-list-item>
                  </v-list>
                </v-bottom-sheet>
              </v-list-item>
            </v-list>
          </v-col>
        </v-row>
      </v-container>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'
import { compress, urltoBlob, downloadFile, EImageType } from 'image-conversion'
@Component
export default class LogoCard extends Vue {
  @Prop({ type: String, required: true, default: '' }) title!: string
  @Prop({ type: String, required: true, default: '' }) path!: string
  @Prop({ type: Boolean, required: false, default: false }) dark!: boolean
  ownvalue: number = 1024
  resolutions: Array<{ text: string, value: number }> = [
    {
      text: 'Высота 16пкс',
      value: 16
    },
    {
      text: 'Высота 32пкс',
      value: 32
    },
    {
      text: 'Высота 64пкс',
      value: 64
    },
    {
      text: 'Высота 128пкс',
      value: 128
    },
    {
      text: 'Высота 256пкс',
      value: 256
    },
    {
      text: 'Высота 512пкс',
      value: 512
    },
    {
      text: 'Высота 1024пкс',
      value: 1024
    },
    {
      text: 'Высота 2048пкс',
      value: 2048
    },
    {
      text: 'Высота 4096пкс',
      value: 4096
    }
  ]
  async getImage (type: string, value: number) {
    let scaling = value / 4096
    console.log(`resize ${type} to ${value} and download, scaling to ${scaling}`)
    let image = await urltoBlob(`${this.path}.${type}`)
    let compressed = await compress(image, {
      quality: 0.9,
      scale: scaling,
      type: type === 'jpg' ? EImageType.JPEG : EImageType.PNG
    })
    let name = this.path.split('/').pop()
    downloadFile(compressed, `${name}_h${value}.${type}`)
  }
}
</script>

<style>
</style>