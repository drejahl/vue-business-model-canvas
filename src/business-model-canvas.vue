<template>
  <v-container fluid grid-list-md>
    <v-layout column>
      <v-layout row wrap>
        <v-flex d-flex xs12 sm6 md2>
          <BmcKeyPartners :partners="canvas.keyPartners" :businessModel="canvas" :editable="editable" :enableComments="enableComments"
            @newPartnerRating="newPartnerRating" @newPartnerComment="newPartnerComment" @displayComments="displayComments">
          </BmcKeyPartners>
        </v-flex>
        <v-flex d-flex xs12 sm6 md2>
          <v-layout row wrap>
            <v-flex d-flex>
              <v-layout row wrap>
                <v-flex d-flex xs12>
                  <BmcKeyActivities :activities="canvas.keyActivities":editable="editable" :enableComments="enableComments"
                    @newActivityRating="newActivityRating" @newActivityComment="newActivityComment" @displayComments="displayComments">
                  </BmcKeyActivities>
                </v-flex>
                <v-flex d-flex xs12>
                  <BmcKeyResources :resources="canvas.keyResources":editable="editable" :enableComments="enableComments"
                    @newResourceRating="newResourceRating" @newResourceComment="newResourceComment" @displayComments="displayComments">
                  </BmcKeyResources>
                </v-flex>
              </v-layout>
            </v-flex>
          </v-layout>
        </v-flex>
        <v-flex d-flex xs12 sm6 md2>
          <BmcValuePropositions :propositions="canvas.valuePropositions" :editable="editable" :enableComments="enableComments"
            @newPropositionRating="newPropositionRating" @newPropositionComment="newPropositionComment" @displayComments="displayComments">
          </BmcValuePropositions>
        </v-flex>
        <v-flex d-flex xs12 sm6 md2>
          <v-layout row wrap>
            <v-flex d-flex>
              <v-layout row wrap>
                <v-flex d-flex xs12>
                  <BmcCustomerRelationships :relationships="canvas.customerRelationships" :editable="editable" :enableComments="enableComments"
                    @newCustRelRating="newCustRelRating" @newCustRelComment="newCustRelComment" @displayComments="displayComments">
                  </BmcCustomerRelationships>
                </v-flex>
                <v-flex d-flex xs12>
                  <BmcChannels :channels="canvas.channels" :editable="editable" :enableComments="enableComments"
                    @newChannelRating="newChannelRating" @newChannelComment="newChannelComment" @displayComments="displayComments">
                  </BmcChannels>
                </v-flex>
              </v-layout>
            </v-flex>
          </v-layout>
        </v-flex>
        <v-flex d-flex xs12 sm6 md2>
          <BmcCustomerSegments :segments="canvas.customerSegments" :businessModel="canvas" :editable="editable" :enableComments="enableComments"
            @newSegmentRating="newSegmentRating" @newSegmentComment="newSegmentComment" @displayComments="displayComments">
          </BmcCustomerSegments>
        </v-flex>
        <v-flex v-if="enableComments && comments" d-flex xs12 sm6 md2>
          <v-layout column style="max-height: 750px;overflow:scroll;">
            <v-card v-for="comment in comments._embedded.item" :key="comment.id" v-if="!comment.subRefId">
              <v-card-title>
                <v-chip>
                  <v-avatar>
                    <img :src="comment.pictureURL" alt="user">
                  </v-avatar>
                  {{comment.userName}}
                </v-chip>
                <div style="text-align: left;">
                  <span class="grey--text">{{formatedDate(comment.created, "DD-MM-YYYY HH:mm:ss")}}</span><br>
                  <span class="grey--text">{{comment.refType}}</span><br>
                  <span>{{comment.body}}</span>
                  <star-rating v-if="comment.rating" :star-size="25" :rating="comment.rating" :read-only="true" :increment="0.01"></star-rating>
                </div>
              </v-card-title>
            </v-card>
          </v-layout>
        </v-flex>
      </v-layout>
      <v-layout row wrap>
        <v-flex d-flex xs12 sm5 md5>
          <BmcCostStructure :costs="canvas.costStructure" :businessModel="canvas" :editable="editable" :enableComments="enableComments"
            @newCostRating="newCostRating" @newCostComment="newCostComment" @displayComments="displayComments">
          </BmcCostStructure>
        </v-flex>
        <v-flex d-flex xs12 sm5 md5>
          <v-card color="blue lighten-2" dark>
            <BmcRevenueStreams :revenues="canvas.revenueStreams" :editable="editable" :enableComments="enableComments"
              @newRevenueRating="newRevenueRating" @newRevenueComment="newRevenueComment" @displayComments="displayComments">
            </BmcRevenueStreams>
          </v-card>
        </v-flex>
      </v-layout>
    </v-layout>
    <v-layout style="text-align: left;">
      <p>Business Model Canvas Business Model Canvas by <a href="https://strategyzer.com/">Alexander Osterwalder</a>.</br>
The business model canvas itself is licensed under the <a href="https://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-Share Alike 3.0 Unported License</a>.</p>
    </v-layout>
    <v-dialog v-model="commentDialog" persistent max-width="500px">
      <v-card>
        <v-card-title>
          <span class="headline">Comments</span>
        </v-card-title>
      </v-card>
      <div if="comments">
        <v-card v-for="comment in comments._embedded.item" :key="comment.id" v-if="comment.subRefId && comment.subRefId===elementId">
          <v-card-title>
            <v-chip>
              <v-avatar>
                <img :src="comment.pictureURL" alt="user">
              </v-avatar>
              {{comment.userName}}
            </v-chip>
            <div style="text-align: left;">
              <span class="grey--text">{{formatedDate(comment.created, "DD-MM-YYYY HH:mm:ss")}}</span><br>
              <span class="grey--text">{{comment.refType}}</span><br>
              <span>{{comment.body}}</span>
              <star-rating v-if="comment.rating" :star-size="25" :rating="comment.rating" :read-only="true" :increment="0.01"></star-rating>
            </div>
          </v-card-title>
        </v-card>
      </div>
      <v-card>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click.native="closeModal">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
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
import fecha from 'fecha'
import StarRating from 'vue-star-rating'

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
    BmcRevenueStreams,
    StarRating
  },
  props: {
    'canvas': Object,
    'enableComments': Boolean,
    'comments': Object,
    'editable': Boolean
  },
  data () {
    return {
      commentDialog: false,
      elementId: null
    }
  },
  methods: {
    formatedDate: function(d,f){
      return fecha.format( parseInt(d),f);
    },
    newCostRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newCostComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newChannelRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newChannelComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newCustRelRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newCustRelComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newSegmentRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newSegmentComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newActivityRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newActivityComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newPartnerRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newPartnerComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newResourceRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newResourceComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newRevenueRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newRevenueComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    newPropositionRating: function(e) {
      this.$emit( "newBmcRating", e)
    },
    newPropositionComment: function(e) {
      this.$emit( "newBmcComment", e)
    },
    displayComments: function(e) {
      this.elementId = e.id;
      this.commentDialog = true;
    },
    closeModal: function() {
      this.commentDialog = false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.sic-card-body {
  padding-top: 5px;
  padding-bottom: 5px;
  padding-left: 5px;
  padding-right: 5px;
  text-align: left;
}

.sic-card-name {
  font-size: 14px;
  font-weight: 500;
  margin-bottom: 5px;
  margin-right: 0px;
  margin-left: 0px;
}
.sic-card-text {
  font-size: 12px;
  font-weight: 400;
  margin-bottom: 5px;
  margin-right: 0px;
  margin-left: 0px;
}
.sic-card-chip {
  background-color: white;
  font-size: 12px;
  color: black;
  height: 18px;
  border-radius: 9px;
  display: inline-block;
  padding-left: 8px;
  padding-right: 8px;
  margin-bottom: 5px;
  margin-right: 3px;
}
</style>
