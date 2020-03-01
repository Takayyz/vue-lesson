<template>
  <div>
    <h1
      class="main_title"
      v-html="leads.message"
      :class="classObj"
    ></h1>
    <p>{{ leads.description }}</p>
    <button
      @click="addDescription"
    >
      add discription
    </button>
    <button @click="changeTextSize">Large</button>
    <hr>
    <child-component
      v-if="isShow"
    >
      <template #head>
        <p>head slot</p>
      </template>
      <template #default>
        <p>main slot</p>
        <p>main slot2</p>
      </template>
      <template #foot>
        <p>foot slot</p>
      </template>
      <!-- <span>こっちは勝手に追加</span> -->
    </child-component>
    <button @click="toggleShow">toggle isShow</button>
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
      <counter></counter>
      <hr>
      <input type="text" v-model="inputText">
      <p>computed: {{ getUpperCaseText }}</p>
      <p>methods: {{ showUpperCaseText() }}</p>
      <hr>
      <form>
        <div>
          <span>名前:</span>
          <input-text v-model="form.name"></input-text>
          <p>名前: {{ getInputName }}</p>
        </div>
        <div>
          <span>性別:</span>
          <label>
            男性
            <input type="radio" value="male" v-model="form.sex">
          </label>
          <label>
            女性
            <input type="radio" value="female" v-model="form.sex">
          </label>
          <p>性別: {{ getRadioValue }}</p>
        </div>
        <div>
          <select v-model="form.selected">
            <option disabled value="">--出身地を選択してください--</option>
            <option>東京都</option>
            <option>埼玉県</option>
            <option>神奈川県</option>
            <option>千葉県</option>
            <option>山形県</option>
          </select>
          <p>出身地: {{ getSelectedValue }}</p>
        </div>
        <div>
          <label>
            <input type="checkbox" v-model="form.checked">
            20歳以上です
          </label>
          <p>チェックボックス: {{ getCheckBoxValue }}</p>
        </div>
      </form>
      <template v-for="category in categories">
        <p :key="$uuid.v4()">
          {{ category }}
        </p>
      </template>
      <button @click="updateText">update text</button>
    </ul>
    <article v-for="post in posts"
      :key="$uuid.v4()"
    >
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
    </article>
  </div>
</template>

<script>
import ChildComponent from 'Components/ChildComponent';
import Counter from 'Components/Counter';
import InputText from 'Components/InputText';
import axios from 'axios';

export default {
  beforeCreate() {
    console.log('beforeCreate');
    // console.log(this.leads); // undefined
  },
  created() {
    console.log('created');
    console.log(this.posts);
    axios.get('/data.json').then(res => {
      this.posts = res.data.posts;
    });
  },
  beforeMount() {
    console.log('beforeMount');
    console.log(this.$el); // undefined
  },
  mounted() {
    console.log('mounted');
    console.log(this.$el);
  },
  beforeUpdate() {
    console.log('beforeUpdate');
  },
  updated() {
    console.log('updated');
  },
  data() {
    return {
      leads: {
        message: '<span>Hello my name is Taka</span>',
        description: '',
      },
      isShow: true,
      id: 2,
      // count: 0, // store管理のため削除
      inputText: '',
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
      form: {
        name: '',
        sex: '',
        selected: '',
        checked: false,
      },
      categories: ['JavaScript', 'jQuery'],
      posts: [],

    }
  },
  methods: {
    incrementCount() {
      console.log('incrementCount');
      this.count++;
    },
    showUpperCaseText() {
      const upperCaseText = this.inputText.toUpperCase();
      // console.log(`method: ${upperCaseText}`);
      return upperCaseText;
    },
    addDescription() {
      // console.log('adDescription');
      this.leads.description = 'Vue-lesson'
      // console.log(this.description);
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
    },
    toggleShow() {
      this.isShow = !this.isShow;
    }
  },
  watch: {
    inputText(value, oldValue) {
      console.log(`value => ${value}`);
      console.log(`oldValue => ${oldValue}`);
    },
    'leads.description': {
      handler() {
        console.log('add description');
      },
      deep: true,
    }
  },
  computed: {
    getUpperCaseText() {
      const upperCaseText = this.inputText.toUpperCase();
      // console.log(`computed: ${upperCaseText}`);
      return upperCaseText;
    },
    getInputName() {
      return this.form.name;
    },
    getRadioValue() {
      return this.form.sex;
    },
    getSelectedValue() {
      return this.form.selected;
    },
    getCheckBoxValue() {
      return this.form.checked;
    }
  },
  components: {
    ChildComponent,
    Counter,
    InputText,
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