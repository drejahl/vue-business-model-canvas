<template>
  <v-container fluid grid-list-md>
    <v-layout row wrap>
      <v-flex d-flex xs12 sm6 md2>
        <BmcKeyPartners :partners="canvas.keyPartners" :businessModel="canvas"/>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2>
        <v-layout row wrap>
          <v-flex d-flex>
            <v-layout row wrap>
              <v-flex d-flex xs12>
                <BmcKeyActivities :activities="canvas.keyActivities"/>
              </v-flex>
              <v-flex d-flex xs12>
                <BmcKeyResources :resources="canvas.keyResources"/>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-layout>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2>
        <BmcValuePropositions :propositions="canvas.valuePropositions"/>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2 child-flex>
        <v-layout row wrap>
          <v-flex d-flex>
            <BmcCustomerRelationships :relationships="canvas.customerRelationships"/>
          </v-flex>
          <v-flex d-flex>
            <BmcChannels :channels="canvas.channels"/>
          </v-flex>
        </v-layout>
      </v-flex>
      <v-flex d-flex xs12 sm6 md2>
        <BmcCustomerSegments :segments="canvas.customerSegments" :businessModel="canvas"/>
      </v-flex>
    </v-layout>
    <v-layout row wrap>
      <v-flex d-flex xs12 sm5 md5>
        <BmcCostStructure :costs="canvas.costStructure" :businessModel="canvas"/>
      </v-flex>
      <v-flex d-flex xs12 sm5 md5>
        <v-card color="blue lighten-2" dark>
          <BmcRevenueStreams :revenues="canvas.revenueStreams"/>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import BmcKeyPartners from './bmc-key-partners.vue';
import BmcKeyActivities from './bmc-key-activities.vue';
import BmcKeyResources from './bmc-key-resources.vue';
import BmcValuePropositions from './bmc-value-propositions.vue';
import BmcCustomerRelationships from './bmc-customer-relationships.vue';
import BmcChannels from './bmc-channels.vue';
import BmcCustomerSegments from './bmc-customer-segments.vue';
import BmcCostStructure from './bmc-cost-structure.vue';
import BmcRevenueStreams from './bmc-revenue-streams.vue';

export default {
  name: 'VueBusinessModelCanvas',
  components: {
    BmcKeyPartners,
    BmcKeyActivities,
    BmcKeyResources,
    BmcValuePropositions,
    BmcCustomerRelationships,
    BmcChannels,
    BmcCustomerSegments,
    BmcCostStructure,
    BmcRevenueStreams
  },
  props: {
    'canvas': Object
  },
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
