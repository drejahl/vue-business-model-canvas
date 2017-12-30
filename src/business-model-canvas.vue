<template>
  <div class="bmc">
    <h1>{{canvas.name}}</h1>
    <container xl="1200">
      <row>
        <column :sm="2" :md="2" class="high-box">
          <div class="bmc-area">
            <bmcTitle @add="addPartner">Partner</bmcTitle>
            <bmcCard v-for="card in canvas.partners" :card="card" :key="card.id"/>
          </div>
        </column>
        <column :sm="2" :md="2">
          <row>
            <column :sm="10" :md="10" class="box">
              <div class="bmc-area">
                <bmcTitle>Key Activities</bmcTitle>
              </div>
            </column>
          </row>
          <row>
            <column :sm="10" :md="10" class="box">
              <div class="bmc-area">
                <bmcTitle>Key Resources</bmcTitle>
              </div>
            </column>
          </row>
        </column>
        <column :sm="2" :md="2" class="high-box">
          <div class="bmc-area">
            <bmcTitle>Value Proposition</bmcTitle>
          </div>
        </column>
        <column :sm="2" :md="2">
          <row>
            <column :sm="10" :md="10" class="box">
              <div class="bmc-area">
                <bmcTitle>Customer Relation</bmcTitle>
              </div>
            </column>
          </row>
          <row>
            <column :sm="10" :md="10" class="box">
              <div class="bmc-area">
                <bmcTitle>Channels</bmcTitle>
              </div>
            </column>
          </row>
        </column>
        <column :sm="2" :md="2" class="high-box">
          <div class="bmc-area">
            <bmcTitle>Customer Segments</bmcTitle>
          </div>
        </column>
      </row>
      <row>
        <column :sm="5" :md="5" class="box">
          <div class="bmc-area">
            <bmcTitle>Costs</bmcTitle>
          </div>
        </column>
        <column :sm="5" :md="5" class="box">
          <div class="bmc-area">
            <bmcTitle>Revenues</bmcTitle>
          </div>
        </column>
      </row>
    </container>
  </div>
</template>

<script>
import bmcTitle from './bmc-title.vue';
import bmcCard from './bmc-card.vue';

export default {
  name: 'bmc',
  components: {
    bmcTitle,
    bmcCard
  },
  props: {
    canvas: Object
  },
  data () {
    return {
    }
  },
  methods: {
    addPartner: function() {
      console.log("Add partner");
      let partner = {"description": "New partner"};
      this.canvas.partners.push(partner);
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

.bmc-area {
  margin: 5px;
  background-color: white;
  border-width: 1px;
  border-style: solid;
  border-color: black;
}

.box {
  border-width: 0px;
  border-style: solid;
  border-color: black;
  background-color: lightgrey;
  height: 100px;
}

.high-box {
  padding-left: -10px;
  border-width: 0px;
  border-style: solid;
  border-color: black;
  background-color: lightgrey;
  height: 200px;
}
</style>
