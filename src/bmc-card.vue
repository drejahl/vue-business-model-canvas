<template>
  <div class="bmc-card">
    <p class="card-text">{{card.description}}  <button @click="remove">-</button></p>
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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.label-text {
  font-weight: bold;
}
</style>
