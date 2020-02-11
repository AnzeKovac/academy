<template>
  <div id="app">
    <navbar></navbar>  
    <div class="container p-3">
      <div class="row">
        <div class="col-8"><course></course></div>
        <div class="col"><lecture-overview></lecture-overview></div>
      </div>
      
      
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Course from './components/Course.vue'
import LectureOverview from './components/LectureOverview.vue'

export default {
  name: 'app',
  components: {
    Navbar,
    Course,
    LectureOverview
  }
}
</script>

<style>
</style>
