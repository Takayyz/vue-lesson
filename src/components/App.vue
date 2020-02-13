<template>
  <div>
    <h1
      class="main_title"
      v-html="message"
      :class="classObj"
    ></h1>
    <p>{{ description }}</p>
    <button
      @click="addDescription"
    >
      add discription
    </button>
    <button @click="changeTextSize">Large</button>
    <hr>
    <child-component
      v-show="isShow"
    >
      <template v-slot:head>
        <p>head slot</p>
      </template>
      <template v-slot:default>
        <p>main slot</p>
        <p>main slot2</p>
      </template>
      <template v-slot:foot>
        <p>foot slot</p>
      </template>
      <!-- <span>こっちは勝手に追加</span> -->
    </child-component>
    <hr>
    <p v-if="id === 1">1</p>
   <template v-else-if="id === 2">
     <p>2-1</p>
     <p>2-2</p>
     <p>2-3</p>
   </template>
    <p v-else>other</p>
    <hr>
    <ul>
      <!-- <template v-for="item in items">
        <li :key="item.id">
          {{ item.title }}
        </li>
      </template> -->
      <template v-for="item in items">
        <child-component
          :key="item.id"
          :title="item.title"
        >
          <span>slot content</span>
        </child-component>
      </template>
      <hr>
      <button @click="incrementCount">Add to count</button>
      <p>{{ count }}回目！！</p>
      <hr>
      <input type="text" v-model="inputText">
      <p>computed: {{ getUpperCaseText }}</p>
      <p>methods: {{ showUpperCaseText() }}</p>
      <hr>
      <template v-for="category in categories">
        <p :key="$uuid.v4()">
          {{ category }}
        </p>
      </template>
      <button @click="updateText">update text</button>
    </ul>
  </div>
</template>

<script>
import ChildComponent from 'Components/ChildComponent';

export default {
  data() {
    return {
      message: '<span>Hello my name is Taka</span>',
      isShow: true,
      id: 2,
      count: 0,
      inputText: '',
      description: '',
      classObj: {
        'is-green': true,
      },
      items: [
        {
          id: this.$uuid.v4(),
          title: '1番目のリスト',
        },
        {
          id: this.$uuid.v4(),
          title: '2番目のリスト',
        },
        {
          id: this.$uuid.v4(),
          title: '3番目のリスト',
        },
      ],
      categories: ['JavaScript', 'jQuery'],
    }
  },
  methods: {
    incrementCount() {
      console.log('incrementCount');
      this.count++;
    },
    showUpperCaseText() {
      const upperCaseText = this.inputText.toUpperCase();
      console.log(`method: ${upperCaseText}`);
      return upperCaseText;
    },
    addDescription() {
      console.log('adDescription');
      this.description = 'Vue-lesson'
      console.log(this.description);
    },
    updateText() {
      console.log('updateText');
      // this.categories.splice(1, 1, 'Vue.js');

      // スプレッド演算子パターン
      // this.classObj = {...this.classObj, 'is-large': true}

      // $setパターン
      this.$set(this.classObj, 'is-large', true);

      this.$set(this.categories, 1, 'Vue.js');
    },
    changeTextSize() {
      this.classObj = Object.assign({}, this.classObj, {
        'is-large': true,
      });
    }
  },
  computed: {
    getUpperCaseText(){
      const upperCaseText = this.inputText.toUpperCase();
      console.log(`computed: ${upperCaseText}`);
      return upperCaseText;
    }
  },
  components: {
    ChildComponent,
  }
}
</script>

<style scoped>
  .main_title {
    text-align: center;
  }
  .is-green {
    color: green;
  }
  .is-large {
    font-size: 48px;
  }
  hr {
    margin: 16px 0;
  }
</style>