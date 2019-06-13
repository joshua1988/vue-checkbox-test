<template>
  <div>
    <check-box label="all" v-model="all"></check-box>
    <check-box label="check1" v-model="check1"></check-box>
    <check-box label="check2" v-model="check2"></check-box>
    <check-box label="check3" v-model="check3"></check-box>
  </div>
</template>

<script>
// NOTE: 개별 컴포넌트로 분리한 경우
import CheckBox from './components/CheckBox.vue';

export default {
  components: {
    CheckBox
  },
  data() {
    return {
      all: false,
      check1: false,
      check2: false,
      check3: false,
    }
  },
  watch: {
    all(value) {
      this.check1 = value;
      this.check2 = value;
      this.check3 = value;
    },
    check3(value) {
      this.check1 = value;
    }
  }
}
</script>

<style>

</style>
