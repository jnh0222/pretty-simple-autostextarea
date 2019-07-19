<template>
<div>
    <textarea
    ref="message"
    v-model="message"
    @input="handleInput"
    rows="1"
    class="hw-auto-textarea"
    :placeholder="placeholder"></textarea>
</div>
</template>

<script>
const initScrollHeight = 21;
const padding = 12; // border width(2) + vertical padding(5*2)

export default {
  name: 'autosize-textarea',
  data() {
    return {
      message: this.parentMessage,
    }
  },
  watch: {
    parentMessage(newVal) {
      this.message = newVal;
    }
  },
  updated() {
    this.autoSize();
  },
  props: {
    'parentMessage': {type: String, required: true},
    'maxRow': {type: Number, required: false, default: 5},
    'width': {type: String, required: false, default: '100%'},
    'placeholder': {type: String, required: false, default: ''},
  },
  methods: {
    handleInput(e) {
      this.message = e.target.value;
      this.$emit('input', this.message);
    },
    autoSize() {
      var el = this.$refs.message;
      var maxHeight = initScrollHeight * this.maxRow + padding;

      setTimeout(function(){
        if(el.scrollHeight < maxHeight) {
          el.style.height = 'auto';
          el.style.height = `${el.scrollHeight + 3}px`;
          el.style.overflowY = 'hidden';
        } else {
          el.style.height = `${maxHeight}px`;
          el.style.overflowY = 'scroll';
        }
      }, 0);
    },
  },
  mounted() {
    // initialize width
    this.$refs.message.style.width = this.width;

    this.autoSize();
  }
}
</script>

<style lang="scss" scoped>
.hw-auto-textarea {
  width: 100%;
  height: 34px;
  min-height:0;
  overflow:hidden;
  resize: none;
  padding: 5px 10px;
  font-size: 14px;
  border: 1px solid #d6d6d6;
  transition-duration: .2s;
}
</style>
