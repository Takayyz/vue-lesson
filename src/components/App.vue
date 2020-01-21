<template>
  <div>
    <h1>{{message}}</h1>
    <hr>
    <child-component></child-component>
  </div>
</template>

<script>
import ChildComponent from 'Components/ChildComponent';

export default {
  data() {
    return {
      message: 'Hello my name is Taka',
    }
  },
  components: {
    ChildComponent,
  }
}
</script>

<style scoped>
  h1 {
    color: green;
  }
  hr {
    margin: 16px 0;
  }
</style>