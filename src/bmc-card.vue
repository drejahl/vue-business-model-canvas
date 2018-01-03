<template>
  <div>
    <p v-bind:style="styleObject">{{card.description}}<button class="btn-sm" @click="remove">-</button></p>
  </div>
</template>

<script>
export default {
  name: 'bmc-card',
  props: {
    card: Object
  },
  methods: {
    remove: function() {
      this.$emit('removeCard');
    }
  },
  computed: {
    styleObject: function () {
      return {
        'background-color': this.card.color,
        'margin-left': "10%",
        'margin-right': "10%",
        'padding-top': "5px",
        'padding-bottom': "5px",
        'border-radius': "10px",
        'box-shadow': '0px 6px 20px ' + this.card.color,
        'font-size': "10px"
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.label-text {
  font-weight: bold;
}
.btn-sm {
  float: right;
  font-size: 8px;
  margin-left: 10px;
  margin-right: 10px;
}
</style>
