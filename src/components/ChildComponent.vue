<template>
  <div class="wrapper">
    <h2>{{ title }}</h2>
    <slot name="head"></slot>
    <slot>default slot</slot>
    <!-- <slot></slot> -->
    <slot name="foot"></slot>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
    }
  }
}
</script>

<style scoped>
  .wrapper {
    text-align: center;
  }
</style>