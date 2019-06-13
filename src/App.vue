<template>
  <div id="app">
    <input type="checkbox" id="all" @change="checkAll">
    <label for="all">All</label>
    <input type="checkbox" id="box1" v-model="check1">
    <label for="box1">code1</label>
    <input type="checkbox" id="box2" v-model="check2">
    <label for="box2">code2</label>
    <input type="checkbox" id="box3" v-model="check3">
    <label for="box3">code3</label>
  </div>
</template>

<script>
// NOTE: 컴포넌트로 분리하지 않은 경우
export default {
  data() {
    return {
      all: null,
      check1: null,
      check2: null,
      check3: null,
    }
  },
  watch: {
    check3(value) {
      if (value) {
        this.check1 = true;
      }
    }
  },
  methods: {
    checkAll() {
      this.check1 = event.target.checked;
      this.check2 = event.target.checked;
      this.check3 = event.target.checked;
    }
  }
}
</script>
