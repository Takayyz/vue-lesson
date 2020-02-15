<template>
  <div>
    <button @click="incrementCount">Add to count</button>
    <p>{{ count }}回目！！</p>
  </div>
</template>

<script>
export default {
  props: {
    count: Number,
  },
  methods: {
    incrementCount() {
      this.$emit('increment');
    }
  }
}
</script>