<template>
  <div id="app">
    <navbar></navbar>  
    <lecture></lecture>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Lecture from './components/Lecture.vue'

export default {
  name: 'app',
  components: {
    Navbar,
    Lecture
  }
}
</script>

<style>
</style>
