<template>
  <v-card color="grey lighten-2">
    <v-toolbar flat color="grey darken-1" dark height="40px">
      <!--v-toolbar-side-icon></v-toolbar-side-icon-->
      <v-btn v-if="editable" icon style="margin-left: 0px;" @click.native.stop="create">
        <v-icon>add</v-icon>
      </v-btn>
      <v-toolbar-title style="margin-left: 0px;" class="body-1">Channels</v-toolbar-title>
    </v-toolbar>
    <v-layout row wrap style="min-height: 50px;">
      <v-flex xs12 v-for="(p,i) in channels" :key="p.id">
        <v-card color="teal lighten-2" class="white--text">
          <v-toolbar flat color="teal lighten-1" dark height="20px">
            <v-btn v-if="editable" flat dark icon small style="margin-left: 0px;" @click.native.stop="edit(i)">
              <v-icon size="16px">edit</v-icon>
            </v-btn>
            <v-btn v-if="enableComments" flat dark icon small style="margin-left: 0px;" @click.native.stop="$emit('newChannelComment', p)">
              <v-icon size="16px">add_comment</v-icon>
            </v-btn>
            <v-btn v-if="enableComments && p.id" flat dark icon small style="margin-left: 0px;" @click.native.stop="$emit('newChannelRating', p)">
              <ion-icon name="star-outline" style="font-size: 16px;margin-bottom: 3px;"></ion-icon>
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn v-if="enableComments && p.id" flat dark icon small style="margin-left: 0px;" @click.native.stop="$emit('displayComments', p)">
              <ion-icon name="chatboxes" style="font-size: 16px;margin-bottom: 3px;"></ion-icon>
            </v-btn>
            <v-btn v-if="editable" flat dark icon small style="margin-right: 0px;" @click.native.stop="del(i)">
              <v-icon size="16px">clear</v-icon>
            </v-btn>
          </v-toolbar>
          <div class="sic-card-body">
            <p class="sic-card-name">{{p.name}}</p>
            <p class="sic-card-text">{{p.description}}</p>
            <div v-for="t in p.type" class="sic-card-chip">{{t}}</div>
          </div>
        </v-card>
      </v-flex>
    </v-layout>
    <v-dialog v-model="dialog" persistent max-width="500px">
      <v-card>
        <v-card-title>
          <span class="headline">Channel</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm12 md8>
                <v-text-field label="Name" required v-model="channel.name"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6>
                <v-select label="Type" multiple autocomplete chips v-model="channel.type"
                  :items="['Online', 'Direct', 'Indirect', 'Delivery']">
                </v-select>
              </v-flex>
              <v-flex xs12 sm12 md12>
                <v-text-field multi-line label="Description" v-model="channel.description"></v-text-field>
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
  name: 'BmcChannels',
  components: {
  },
  props: {
    'channels': Array,
    'enableComments': Boolean,
    'editable': Boolean
  },
  data () {
    return {
      dialog: false,
      editIdx: null,
      channel: {description:""}
    }
  },
  mounted: function() {
  },
  methods: {
    del: function(i) {
      this.channels.splice(i, 1);
    },
    close: function() {
      this.dialog=false;
    },
    create: function() {
      this.channel = { type: [] };
      this.dialog=true;
    },
    edit: function(i) {
      this.channel =  Object.assign( {}, this.channels[i]);
      this.editIdx = i;
      this.dialog=true;
    },
    save: function(i) {
      this.dialog=false;

      if (!this.channel.id) {
        this.channel.id=uuidv1();
        this.channels.push(this.channel);
      } else {
        this.channels[this.editIdx] = Object.assign( {}, this.channel);
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
