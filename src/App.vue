<template>
  <div id="app">
    <div class="wrap">
      <h1>simple-textarea</h1>
      <!-- <ul class="input-list">
        <li><label for="inputWidth">width</label><input type="text" id="inputWidth" v-model="inputWidth"></li>
        <li><label for="inputMinRow">minRow</label><input type="text" id="inputMinRow" v-model.number="inputMinRow"></li>
        <li><label for="inputPlaceholder">placeholder</label><input type="text" id="inputPlaceholder" v-model.number="inputPlaceholder"></li>
        <li class="multiline">          
          <div><label for="isAutosize">autosize</label><input type="checkbox" id="isAutosize" v-model="isAutosize"></div>
          <div v-show="isAutosize"><label for="inputMaxrow">maxrow</label><input type="text" id="inputMaxrow" v-model.number="inputMaxrow"></div>
        </li>
      </ul>
      <SimpleTextarea
      :parentMessage="textValue"
      v-model="textValue"
      :placeholder="inputPlaceholder"
      :width="inputWidth"
      :minRow="inputMinRow"
      :autosize="isAutosize || autosizeObject"
      /> -->

      <SimpleTextarea
      :parentMessage="textValue"
      v-model="textValue"
      placeholder="Insert the text."
      :minRow="3"
      :autosize="{'maxRow': 10}"
      />
      <div class="playground">
        <p>{{textValue}}</p>
        <button type="button" @click="appendText">Fetch some text</button>
      </div>
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
      textValue: '체포·구속·압수 또는 수색을 할 때에는 적법한 절차에 따라 검사의 신청에 의하여 법관이 발부한 영장을 제시하여야 한다. 다만, 현행범인인 경우와 장기 3년 이상의 형에 해당하는 죄를 범하고 도피 또는 증거인멸의 염려가 있을 때에는 사후에 영장을 청구할 수 있다. 선거에 관한 경비는 법률이 정하는 경우를 제외하고는 정당 또는 후보자에게 부담시킬 수 없다. 모든 국민은 학문과 예술의 자유를 가진다. 감사원은 세입·세출의 결산을 매년 검사하여 대통령과 차년도국회에 그 결과를 보고하여야 한',
      inputWidth: '100%',
      inputMinRow: 5,
      inputPlaceholder: '',
      // isAutosize: false,
      // inputMaxrow: null,
      // autosizeObject: null
    }
  },
  // watch: {
  //   inputMaxrow() {
  //     if(this.isAutosize) {
  //       this.autosizeObject =  {maxRow: this.inputMaxrow};
  //     }
  //   }
  // },
  methods: {
    appendText() {
      axios.get('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => {
        this.textValue = response.data.title;
      })
    }
  },
  // mounted() {
  //   if(this.isAutosize || _.isObject(this.isAutosize)) {
  //     this.inputMaxrow = null || this.inputMinRow + 5;
  //   }
  // }
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

// .input-list {
//   margin-bottom: 60px;

//   input[type="checkbox"] {
//     width: 16px;
//     height: 16px;
//   }

//   > li {
//     display: flex;
//     align-items: center;
//     margin-bottom: 10px;
//     label {
//       width: 120px;
//       & + input[type="text"],
//       & + input[type="number"] {
//         flex: 1;
//       }
//     }

//     &.multiline {
//       display: block;
//       > div {
//         display: flex;
//         align-items: center;
//         margin-bottom: 10px;
//       }
//     }
//   }
// }

.playground {
  margin-top: 20px;

  p {
    white-space: pre-line;
  }
  
  button {
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
}
</style>
