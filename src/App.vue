<template>
  <div id="app">
    <div class="wrap">
      <AutosizeTextarea :parentMessage="textValue" v-model="textValue" :maxRow="3"/>
      <div class="playground">
        <p>{{textValue}}</p>
        <button type="button" @click="appendText">Fetch some text</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import AutosizeTextarea from './components/AutosizeTextarea.vue'

export default {
  name: 'app',
  components: {
    AutosizeTextarea
  },
  data() {
    return {
      textValue: '체포·구속·압수 또는 수색을 할 때에는 적법한 절차에 따라 검사의 신청에 의하여 법관이 발부한 영장을 제시하여야 한다. 다만, 현행범인인 경우와 장기 3년 이상의 형에 해당하는 죄를 범하고 도피 또는 증거인멸의 염려가 있을 때에는 사후에 영장을 청구할 수 있다. 선거에 관한 경비는 법률이 정하는 경우를 제외하고는 정당 또는 후보자에게 부담시킬 수 없다. 모든 국민은 학문과 예술의 자유를 가진다. 감사원은 세입·세출의 결산을 매년 검사하여 대통령과 차년도국회에 그 결과를 보고하여야 한'
    }
  },
  methods: {
    appendText() {
      axios.get('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => {
        this.textValue = response.data.title;
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.wrap {
  line-height: 1.5;
  padding: 40px;
}

.playground {
  margin-top: 100px;
  
  button {
    margin-top: 40px;
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
}
</style>
