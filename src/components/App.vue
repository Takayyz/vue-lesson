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
      classObj: {
        'is-green': true,
      },
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