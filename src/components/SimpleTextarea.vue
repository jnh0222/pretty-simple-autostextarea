<template>
<div>
    <textarea
    ref="message"
    :value="parentMessage"
    @input="handleInput"
    :rows="minRow"
    class="simple-textarea"
    :class="simpleTextareaClass"
    :placeholder="placeholder"></textarea>
</div>
</template>

<script>
const initScrollHeight = 21;
const padding = 12; // border width(2) + vertical padding(5*2)

export default {
  name: 'simple-textarea',
  watch: {
    parentMessage(newVal) {
      this.$refs.message.value = newVal;
    }
  },
  updated() {
    if(typeof this.autosize == 'boolean' || typeof this.autosize == 'object') {
      this.calcSize();
    }
  },
  props: {
    parentMessage: {type: String, required: true},
    placeholder: {type: String, required: false, default: ''},
    width: {type: String, required: false, default: '100%'},
    minRow: {type: Number, required: false, default: 5},
    autosize: {type: [Boolean, Object], required: false, default: false},
    simpleTextareaClass: {type: String, required: false, default: null}
  },
  methods: {
    handleInput(e) {
      this.$emit('input', e.target.value);
    },
    calcSize() {
      var el = this.$refs.message;

      if(this.autosize === true) {
        setTimeout(function(){
          el.style.height = 'auto';
          el.style.height = `${el.scrollHeight + 3}px`;
          el.style.overflowY = 'hidden';
        }, 0);
      }
      else if(typeof this.autosize == 'object') {
        var maxHeight = initScrollHeight * (this.autosize.maxRow ? this.autosize.maxRow : this.minRow + 5) + padding;
        
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
      }

    },
  },
  mounted() {
    // initialize width
    this.$refs.message.style.width = this.width;

    if(typeof this.autosize == 'boolean' || typeof this.autosize == 'object') {
      this.calcSize();
    }
  }
}
</script>

<style lang="scss" scoped>
.simple-textarea {
  width: 100%;
  overflow: auto;
  resize: none;
  padding: 5px 10px;
  font-size: 14px;
  border: 1px solid #d6d6d6;
  transition-duration: .2s;
}
</style>
