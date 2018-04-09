<template>
  <v-container fluid grid-list-md>
    <v-layout row wrap>
      <v-flex d-flex xs12 sm6 md2>
        <BmcKeyPartners :partners="canvas.keyPartners"/>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2>
        <v-layout row wrap>
          <v-flex d-flex>
            <v-layout row wrap>
              <v-flex d-flex xs12>
                <v-card color="red lighten-2" dark>
                  <v-card-title primary class="title">Key Activities</v-card-title>
                  <v-card-text></v-card-text>
                </v-card>
              </v-flex>
              <v-flex d-flex xs12>
                <v-card color="red lighten-2" dark>
                  <v-card-title primary class="title">Key Resources</v-card-title>
                  <v-card-text></v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-layout>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2>
        <v-card color="red lighten-3">
          <v-toolbar flat color="red lighten-2" dark height="30px">
            <v-toolbar-side-icon></v-toolbar-side-icon>
            <v-toolbar-title  class="body-2">Value Propositions</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-menu offset-y>
              <v-btn icon slot="activator">
                <v-icon>more_vert</v-icon>
              </v-btn>
              <v-list>
                <v-list-tile @click="">
                  <v-list-tile-title>New</v-list-tile-title>
                </v-list-tile>
              </v-list>
            </v-menu>
          </v-toolbar>
          <v-card-text></v-card-text>
        </v-card>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2 child-flex>
        <v-layout row wrap>
          <v-flex d-flex>
            <v-card color="green lighten-2" dark>
              <v-card-title primary class="title">Customer Relationships</v-card-title>
              <v-card-text></v-card-text>
            </v-card>
          </v-flex>
          <v-flex d-flex>
            <v-card color="green lighten-2" dark>
              <v-card-text
              v-text="lorem.slice(0, 90)">
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2>
        <v-card color="teal lighten-3">
          <v-toolbar flat color="teal lighten-2" dark height="30px">
            <v-toolbar-side-icon></v-toolbar-side-icon>
            <v-toolbar-title  class="body-2">Customer Segments</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-menu offset-y>
              <v-btn icon slot="activator">
                <v-icon>more_vert</v-icon>
              </v-btn>
              <v-list>
                <v-list-tile @click="">
                  <v-list-tile-title>New</v-list-tile-title>
                </v-list-tile>
              </v-list>
            </v-menu>
          </v-toolbar>
          <v-card-text></v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
    <v-layout row wrap>
      <v-flex d-flex xs12 sm5 md5>
        <v-card color="purple" dark>
          <v-card-title primary class="title">Lorem</v-card-title>
          <v-card-text>ABC</v-card-text>
        </v-card>
      </v-flex>
      <v-flex d-flex xs12 sm5 md5>
        <v-card color="blue lighten-2" dark>
          <v-card-text
          v-text="lorem.slice(0, 100)">
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import BmcKeyPartners from './bmc-key-partners.vue';

export default {
  name: 'VueBusinessModelCanvas',
  components: {
    BmcKeyPartners
  },
  props: {
    'canvas': Object
  },
  data () {
    return {
      lorem: `Lorem ipsum dolor sit amet, mel at clita quando. Te sit oratio vituperatoribus, nam ad ipsum posidonium mediocritatem, explicari dissentiunt cu mea. Repudiare disputationi vim in, mollis iriure nec cu, alienum argumentum ius ad. Pri eu justo aeque torquatos.`
    }
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
