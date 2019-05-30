<template>
  <div class="checkbox-area">
    <span v-if="includeAll" class="input-checkbox">
      <input type="checkbox" :id="uniqueId + 'all'" :checked="allChecked"
        value=""
        v-on:click="onClickCheckAll"
      />
      <label :for="uniqueId + 'all'">
        {{ placeholder }}
      </label>
    </span>
    <span
      class="input-checkbox"
      v-for="(item, index) in optionList"
      :key="item.code"
    >
      <input
        type="checkbox"
        :id="uniqueId + index"
        :value="item.code"
        v-model.lazy="selected"
        @change="onChange"
      />
      <label :for="uniqueId + index">
        {{ item.desc }}
      </label>
    </span>
  </div>
</template>

<script>
export default {
  name: 'CheckboxBase',
  data() {
    return {
      optionList: [],
      selected: this.value.slice(0), // 단일 선택 : String, 다중 선택 : Array
      allCheck: this.includeAll
    }
  },
  props: {
    value: {
      required: true
    },
    list: { // optionList를 외부에서 받는 경우
      required: true
    },
    // input attribute
    disabled: {
      type: Boolean,
      required: false,
      default: () => false
    },
    placeholder: {
      type: String,
      required: false,
      default: () => 'All'
    },
    // 기타 확장 기능
    includeAll: { // 전체 선택지 유무 (default : 있음)
      type: Boolean,
      required: false,
      default: () => false
    }
  },
  computed: {
    uniqueId: function() {
      return `_input-${this._uid}--`;
    },
    allChecked() {
      return this.includeAll && this.selected.length === this.list.length;
    }
  },
  created() {
    this.initList();
  },
  watch: {
    value: {
      handler: function(newVal, oldVal) {
        if (newVal !== oldVal) {
          this.setSelected();
        }
      },
      deep: true,
      immidiate: true
    },
    list: function() {
      this.initList();
    }
  },
  methods: {
    setSelected: function() {
      this.selected = this.value.slice(0);
    },
    initList: function() {
      if (this.list) {
        this.optionList = this.parseList(this.list);
      }
    },
    parseList: function(list) {
      let newList = [];

      list.forEach(function(val) {
        if (typeof (val) === 'object') {
          newList.push(val);
        } else {
          newList.push({
            code: val,
            desc: val
          });
        }
      });

      return newList;
    },
    onChange: function() {
      this.$emit('input', this.selected);
      this.$emit('change', this.selected);
    },
    onClickCheckAll: function(e) {
      let selectedCodes = [];

      if (e.target.checked) {
        this.list.forEach(function(el) {
          selectedCodes.push(el.code);
        });
      }

      this.selected = selectedCodes;
      this.onChange();
    }
  }
};

</script>

