<template>
  <div id="app">
    <navbar></navbar>  
    <course></course>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Course from './components/Course.vue'

export default {
  name: 'app',
  components: {
    Navbar,
    Course
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: 'Montserrat', sans-serif;
  background-color: #24252A;
}

*{
  margin: 0;
  padding: 0;
}
</style>
