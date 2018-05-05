<template>
  <v-card color="grey lighten-2">
    <v-toolbar flat color="grey darken-1" dark height="40px">
      <!--v-toolbar-side-icon></v-toolbar-side-icon-->
      <v-btn icon style="margin-left: 0px;" @click.native.stop="create">
        <v-icon>add</v-icon>
      </v-btn>
      <v-toolbar-title style="margin-left: 0px;" class="body-1">Customer Segments</v-toolbar-title>
    </v-toolbar>
    <v-layout row wrap style="min-height: 50px;">
      <v-flex xs12 v-for="(p,i) in segments" :key="p.id">
        <v-card color="teal lighten-2" class="white--text">
          <v-toolbar flat color="teal lighten-1" dark height="20px">
            <v-btn flat dark icon small style="margin-left: 0px;" @click.native.stop="edit(i)">
              <v-icon size="16px">edit</v-icon>
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn flat dark icon small style="margin-right: 0px;" @click.native.stop="del(i)">
              <v-icon size="16px">clear</v-icon>
            </v-btn>
          </v-toolbar>
          <div class="sic-card-body">
            <p class="body-2">{{p.name}}</p>
            <p class="sic-card-text">{{p.description}}</p>
            <div v-for="t in p.type" class="sic-card-chip">{{t}}</div>
          </div>
        </v-card>
      </v-flex>
    </v-layout>
    <v-dialog v-model="dialog" persistent max-width="500px">
      <v-card>
        <v-card-title>
          <span class="headline">Customer Segment</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm12 md12>
                <v-text-field label="Name" required v-model="segment.name"></v-text-field>
                <v-select :items="businessModel.channels" v-model="segment.primaryChannelRef"
                  label="Primary channel" item-text="name" multiple chips item-value="id"></v-select>
                <v-select :items="businessModel.channels" v-model="segment.secondaryChannelRef"
                  label="Secondary channel" item-text="name" multiple chips item-value="id"></v-select>
                  <v-select :items="businessModel.customerRelationships" v-model="segment.customerRelationshipRef"
                    label="Associated customer relationships" item-text="name" multiple chips item-value="id"></v-select>
              </v-flex>
              <v-flex xs12 sm6>
                <v-select label="Type" multiple autocomplete chips v-model="segment.type"
                  :items="['Consumer', 'Prosumer', 'SoHo', 'SME', 'Enterprise']">
                </v-select>
              </v-flex>
              <v-flex xs12 sm12 md12>
                <v-text-field multi-line label="Description" v-model="segment.description"></v-text-field>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click.native="close">Cancel</v-btn>
          <v-btn color="blue darken-1" flat @click.native="save">Ok</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
import uuidv1 from 'uuid/v1';

export default {
  name: 'BmcCustomerSegments',
  components: {
  },
  props: {
    'segments': Array,
    'businessModel': Object
  },
  data () {
    return {
      dialog: false,
      editIdx: null,
      segment: {description:"", type: [], promaryChannelRef: [], secondaryChannelRef: [], customerRelationshipRef: []}
    }
  },
  mounted: function() {
  },
  methods: {
    del: function(i) {
      this.segments.splice(i, 1);
    },
    close: function() {
      this.dialog=false;
    },
    create: function() {
      this.segment = { description:"", type: [], promaryChannelRef: [], secondaryChannelRef: [], customerRelationshipRef: [] };
      this.dialog=true;
    },
    edit: function(i) {
      this.segment =  Object.assign( {}, this.segments[i]);
      if (!this.segment.primaryChannelRef) {this.segment.primaryChannelRef=[]}
      if (!this.segment.secondaryChannelRef) {this.segment.secondaryChannelRef=[]}
      if (!this.segment.customerRelationshipRef) {this.segment.customerRelationshipRef=[]}
      this.editIdx = i;
      this.dialog=true;
    },
    save: function(i) {
      this.dialog=false;

      if (!this.segment.id) {
        this.segment.id=uuidv1();
        this.segments.push(this.segment);
      } else {
        this.segments[this.editIdx] = Object.assign( {}, this.segment);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
