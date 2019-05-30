<template>
  <div id="app">
    <checkbox @change="onChange" :list="codeList" v-model="selectedList" :include-all="true"></checkbox>
  </div>
</template>

<script>
import Checkbox from './components/Checkbox'

export default {
  name: 'app',
  components: {
    Checkbox
  },
  data() {
    return {
      codeList: [
        {code: 'code1', desc: 'option1'},
        {code: 'code2', desc: 'option2'},
        {code: 'code3', desc: 'option3'}
      ],
      selectedList: []
    }
  },
  methods: {
    onChange(val) {
      if (val.includes('code3')) {
        let arr = this.selectedList.filter(function(val) {return val !== 'code1'});
        arr.push('code1');
        this.selectedList = arr;
      }
    }
  }
}
</script>
