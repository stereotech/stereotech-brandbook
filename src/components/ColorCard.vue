Skip to content
Search or jump to…
Pull requests
Issues
Marketplace
Explore

@frylock34
stereotech
/
Stereotech-Private-App
Private
1
00
Code
Issues
4
Pull requests
Actions
Projects
Security
Insights
Settings
Stereotech-Private-App/components/colors/ColorCard.vue
@Kate8954
Kate8954 corrected color display
Latest commit 073d248 on 2 Dec 2020
 History
 2 contributors
@Kate8954@frylock34
102 lines (93 sloc)  2.63 KB

<template>
  <v-card>
    <v-card-title>{{ name }}</v-card-title>
    <v-card-text>
      <v-container>
        <v-row justify="center" align="center">
          <v-col cols="12">
            <v-sheet
              elevation="2"
              rounded
              height="100"
              :color="color"
            ></v-sheet>
          </v-col>
          <v-col cols="12">
            <v-text-field
              :id="`${color}-hex`"
              readonly
              :value="color"
              outlined
              label="HEX"
              append-icon="mdi-content-copy"
              @click:append="toclipboard(`${color}-hex`)"
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-text-field
              :id="`${color}-rgb`"
              readonly
              :value="`${rgb.r}, ${rgb.g}, ${rgb.b}`"
              outlined
              label="RGB"
              append-icon="mdi-content-copy"
              @click:append="toclipboard(`${color}-rgb`)"
            ></v-text-field>
          </v-col>
          <v-row>
            <v-text-field
              :id="`${color}-cmyk`"
              readonly
              :value="`${cmyk.c}, ${cmyk.m}, ${cmyk.y}, ${cmyk.k}`"
              outlined
              label="CMYK"
              append-icon="mdi-content-copy"
              @click:append="toclipboard(`${color}-cmyk`)"
            ></v-text-field>
          </v-row>
        </v-row>
      </v-container>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'
@Component
export default class ColorCard extends Vue {
  @Prop({ type: String, required: true, default: '#FF0000' }) color!: string
  @Prop({ type: String, required: false, default: '' }) name!: string
  toclipboard (id: string) {
    let input = document.getElementById(id);
    //@ts-ignore
    input.select();
    document.execCommand("copy");
  }
  get rgb () {
    var result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(this.color);
    return result ? {
      r: parseInt(result[1], 16),
      g: parseInt(result[2], 16),
      b: parseInt(result[3], 16)
    } : null;
  }
  get cmyk () {
    if (this.rgb != null) {
      var c = 1 - (this.rgb.r / 255);
      var m = 1 - (this.rgb.g / 255);
      var y = 1 - (this.rgb.b / 255);
      var k = Math.min(c, Math.min(m, y));
      c = (c - k) / (1 - k);
      m = (m - k) / (1 - k);
      y = (y - k) / (1 - k);
      c = isNaN(c) ? 0 : c;
      m = isNaN(m) ? 0 : m;
      y = isNaN(y) ? 0 : y;
      k = isNaN(k) ? 0 : k;
      return {
        c: c.toFixed(3),
        m: m.toFixed(3),
        y: y.toFixed(3),
        k: k.toFixed(3)
      }
    }
    return null
  }
}
</script>

<style>
</style>