<template>
  <div>
    <h1
      v-html="message"
      :class="classObj"
    ></h1>
    <hr>
    <child-component
      v-show="isShow"
    ></child-component>
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
        <child-component :key="item.id"></child-component>
      </template>
      <hr>
      <button @click="count++">Add to count</button>
      <p>{{ count }}回目！！</p>
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
      ]
    }
  },
  components: {
    ChildComponent,
  }
}
</script>

<style scoped>
  .is-green {
    color: green;
  }
  hr {
    margin: 16px 0;
  }
</style>