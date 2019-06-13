<template>
  <span>
    <label for="box">{{ label }}</label>
    <input type="checkbox" id="box" @change="changeValue" :checked="value">
  </span>
</template>

<script>
export default {
  props: ['label', 'value'],
  methods: {
    changeValue() {
      this.$emit('input', event.target.checked);
    }
  }
}
</script>

<style>

</style>
