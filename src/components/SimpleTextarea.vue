<template>
<div>
    <textarea
    ref="message"
    :value="parentMessage"
    @input="$_handleInput"
    :rows="minRow"
    class="simple-textarea"
    :class="simpleTextareaClass"
    :placeholder="placeholder"></textarea>
</div>
</template>

<script>
export default {
  name: 'simple-textarea',
  watch: {
    parentMessage(newVal) {
      this.$refs.message.value = newVal;
    }
  },
  updated() {
    if(typeof this.autosize == 'boolean' || typeof this.autosize == 'object') {
      this.$_calcSize();
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
  data() {
    return {
      singleRowScrollHeight: null,
      verticalPadding: 0,
      verticalBorderWidth: 0,
    }
  },
  methods: {
    $_handleInput(e) {
      this.$emit('input', e.target.value);
    },
    $_calcSize() {
      var el = this.$refs.message;

      if(this.autosize === true) {
        // infinite expansion
        el.style.height = 'auto';
        el.style.height = `${el.scrollHeight + this.verticalBorderWidth}px`;
        el.style.overflowY = 'hidden';
      }
      else if(typeof this.autosize == 'object') {
        // expansion until maxHeight
        var maxHeight = this.singleRowScrollHeight * (this.autosize.maxRow ? this.autosize.maxRow : this.minRow + 5) + this.verticalPadding + this.verticalBorderWidth;
        
        if(el.scrollHeight < maxHeight) {
          el.style.height = 'auto';
          el.style.height = `${el.scrollHeight + this.verticalBorderWidth}px`;
          el.style.overflowY = 'hidden';
        } else {
          el.style.height = `${maxHeight}px`;
          el.style.overflowY = 'scroll';
        }
      }
    },
    $_getSingleRowHeight() {
      var singleRowTextarea = document.createElement('textarea');
      singleRowTextarea.setAttribute('rows', 1);
      singleRowTextarea.setAttribute('class', 'simple-textarea');
      document.body.appendChild(singleRowTextarea);
      return singleRowTextarea;
    }
  },
  mounted() {
    // initialize width
    this.$refs.message.style.width = this.width;
    
    let singleRowTextarea = this.$_getSingleRowHeight();    
    let computedStyles = window.getComputedStyle(singleRowTextarea);
    this.verticalPadding = parseInt(computedStyles.getPropertyValue('padding-top')) + parseInt(computedStyles.getPropertyValue('padding-bottom'));
    this.verticalBorderWidth = parseInt(computedStyles.getPropertyValue('border-top-width')) + parseInt(computedStyles.getPropertyValue('border-bottom-width'));
    this.singleRowScrollHeight = singleRowTextarea.scrollHeight - this.verticalPadding;
    singleRowTextarea.parentNode && singleRowTextarea.parentNode.removeChild(singleRowTextarea);

    if(typeof this.autosize == 'boolean' || typeof this.autosize == 'object') {
      this.$_calcSize();
    }
  }
}
</script>

<style lang="scss">
.simple-textarea {
  width: 100%;
  overflow: auto;
  resize: none;
  padding: 5px 10px;
  font-size: 14px;
  border: 1px solid #d6d6d6;
  transition-duration: .2s;
  line-height: normal;
}
</style>
