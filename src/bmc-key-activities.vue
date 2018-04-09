<template>
  <v-card color="teal lighten-3">
    <v-toolbar flat color="teal lighten-2" dark height="30px">
      <!--v-toolbar-side-icon></v-toolbar-side-icon-->
      <v-btn icon style="margin-left: 0px;" @click.native.stop="create">
        <v-icon>add</v-icon>
      </v-btn>
      <v-toolbar-title style="margin-left: 0px;" class="body-1">Key Activities</v-toolbar-title>
    </v-toolbar>
    <v-container fluid style="min-height: 0;" grid-list-lg>
      <v-layout row wrap>
        <v-flex xs12 v-for="(p,i) in activities" :key="p.id">
          <v-card color="blue lighten-2" class="white--text">
            <v-toolbar flat color="blue lighten-1" dark height="20px">
              <v-btn flat dark icon small style="margin-left: 0px;" @click.native.stop="edit(i)">
                <v-icon size="16px">edit</v-icon>
              </v-btn>
              <v-toolbar-title style="margin-left: 0px;" class="caption">{{p.name}}</v-toolbar-title>
              <v-spacer></v-spacer>
              <v-btn flat dark icon small style="margin-right: 0px;" @click.native.stop="del(i)">
                <v-icon size="16px">clear</v-icon>
              </v-btn>
            </v-toolbar>
            <v-card-title primary-title>
              <div class="caption">{{p.description}}</div>
            </v-card-title>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
    <v-dialog v-model="dialog" persistent max-width="500px">
      <v-card>
        <v-card-title>
          <span class="headline">Key Activity</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm12 md8>
                <v-text-field label="Name" required v-model="activity.name"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6>
                <v-select label="Type" multiple autocomplete chips v-model="activity.type"
                  :items="['Technology', 'Sales', 'Marketing', 'Operations', 'Strategic']">
                </v-select>
              </v-flex>
              <v-flex xs12 sm12 md12>
                <v-text-field multi-line label="Description" v-model="activity.description"></v-text-field>
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
  name: 'BmcKeyActivities',
  components: {
  },
  props: {
    'activities': Array
  },
  data () {
    return {
      dialog: false,
      editIdx: null,
      activity: {description:""}
    }
  },
  mounted: function() {
  },
  methods: {
    del: function(i) {
      this.activities.splice(i, 1);
    },
    close: function() {
      this.dialog=false;
    },
    create: function() {
      this.activity = {};
      this.dialog=true;
    },
    edit: function(i) {
      this.activity =  Object.assign( {}, this.activities[i]);
      this.editIdx = i;
      this.dialog=true;
    },
    save: function(i) {
      this.dialog=false;

      if (!this.activity.id) {
        this.activity.id=uuidv1();
        this.activities.push(this.activity);
      } else {
        this.activities[this.editIdx] = Object.assign( {}, this.activity);
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
