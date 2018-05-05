<template>
  <v-card color="grey lighten-2">
    <v-toolbar flat color="grey darken-1" dark height="40px">
      <!--v-toolbar-side-icon></v-toolbar-side-icon-->
      <v-btn icon style="margin-left: 0px;" @click.native.stop="create">
        <v-icon>add</v-icon>
      </v-btn>
      <v-toolbar-title style="margin-left: 0px;" class="body-1">Key Partners</v-toolbar-title>
    </v-toolbar>
    <v-layout row wrap style="min-height: 50px;">
      <v-flex xs12 v-for="(p,i) in partners" :key="p.id">
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
          <span class="headline">Key Partner</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm12 md8>
                <v-text-field label="Name" required v-model="partner.name"></v-text-field>
                <v-select :items="businessModel.keyActivities" v-model="partner.activityRef"
                  label="Associated activities" item-text="name" multiple chips item-value="id"></v-select>
                <v-select :items="businessModel.keyResources" v-model="partner.resourceRef"
                  label="Associated resources" item-text="name" multiple chips item-value="id"></v-select>
              </v-flex>
              <v-flex xs12 sm7>
                <v-select label="Type" multiple autocomplete chips v-model="partner.type"
                  :items="['Technology', 'Sales', 'Marketing', 'Operations', 'Strategic']">
                </v-select>
              </v-flex>
              <v-flex xs12 sm7>
                <v-select label="Stakeholder Type" multiple autocomplete chips v-model="partner.stakeholderType"
                  :items="['Internal', '3rd Party']">
                </v-select>
              </v-flex>
              <v-flex xs12 sm12 md12>
                <v-text-field multi-line label="Description" v-model="partner.description"></v-text-field>
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
  name: 'BmcKeyPartners',
  components: {
  },
  props: {
    'partners': Array,
    'businessModel': Object
  },
  data () {
    return {
      dialog: false,
      editIdx: null,
      partner: {description:"", type: [], stakeholderType: [], activityRef: [], resourceRef: []}
    }
  },
  methods: {
    del: function(i) {
      this.partners.splice(i, 1);
    },
    close: function() {
      this.dialog=false;
    },
    create: function() {
      this.partner = { description:"", type: [], stakeholderType: [], activityRef: [], resourceRef: [] };
      this.dialog=true;
    },
    edit: function(i) {
      this.partner =  Object.assign( {}, this.partners[i]);
      if (!this.partner.activityRef) {this.partner.activityRef=[]}
      if (!this.partner.resourceRef) {this.partner.resourceRef=[]}
      this.editIdx = i;
      this.dialog=true;
    },
    save: function(i) {
      this.dialog=false;

      if (!this.partner.id) {
        this.partner.id=uuidv1();
        this.partners.push(this.partner);
      } else {
        this.partners[this.editIdx] = Object.assign( {}, this.partner);
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
