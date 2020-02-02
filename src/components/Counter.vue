<template>
  <div class="page">
    <h1>ACADEMY</h1>
    <button @click="increment()">Clicks: {{ state.count }} Double: {{ state.double }}</button>
  </div>
</template>

<script>
  import { reactive, computed } from "vue"
  export default {
    setup() {
      const state = reactive({
        count: 0,
        double: computed(() => state.count * 2)
      })

      function increment() {
        state.count++;
      }

      return { state, increment }
    }
  }
</script>

<style>
</style>