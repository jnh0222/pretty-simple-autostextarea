<template>
  <div id="app">
    <div class="wrap">
      <h1>simple-textarea</h1>

      <section class="item">
        <SimpleTextarea
        :parentMessage="textValue1"
        v-model="textValue1"
        placeholder="Default"
        simpleTextareaClass="simple-class"
        />
        <button type="button" class="btn-fetch" @click="appendText(1)">Fetch some text</button>
      </section>

      <section class="item">
        <SimpleTextarea
        :parentMessage="textValue2"
        v-model="textValue2"
        placeholder="minRow: 5(default), maxRow: 10"
        :autosize="{'maxRow': 10}"
        simpleTextareaClass="simple-class"
        />
        <button type="button" class="btn-fetch" @click="appendText(2)">Fetch some text</button>
      </section>

      <section class="item">
        <SimpleTextarea
        :parentMessage="textValue3"
        v-model="textValue3"
        placeholder="minRow: 1"
        :minRow="1"
        autosize
        simpleTextareaClass="simple-class"
        />
        <button type="button" class="btn-fetch" @click="appendText(3)">Fetch some text</button>
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SimpleTextarea from './components/SimpleTextarea.vue'

export default {
  name: 'app',
  components: {
    SimpleTextarea
  },
  data() {
    return {
      textValue1: '',
      textValue2: '',
      textValue3: ''
    }
  },
  methods: {
    appendText(id) {
      axios.get('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => {
        this[`textValue${id}`] = response.data.title;
      })
    }
  }
}
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
  font-size: 3em;
  font-weight: bold;
  margin-bottom: 1.5em;
}

.wrap {
  line-height: 1.5;
  padding: 40px;
}

.item {
  margin-bottom: 60px;
}
  
.btn-fetch {
  margin-top: 20px;
  padding: 1em;
  background-color: #333;
  color: #fff;
  font-weight: bold;
  transition: background-color 0.3s;
  outline: none;
  &:focus, &:hover, &:active {
    background-color: lighten(#333, 10%);
  }
}
</style>
