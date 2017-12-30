<template>
  <div class="bmc-label">
    <p class="label-text"><slot></slot>  <button @click="add">+</button></p>
  </div>
</template>

<script>
export default {
  name: 'bmc-title',
  methods: {
    add: function() {
      this.$emit('add');
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
