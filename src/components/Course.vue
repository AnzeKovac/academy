<template>
  <div class="course">
    <div class="player">
      <video ref="videoPlayerRef" class="video-js"></video>
    </div>
    <div class="course-overview">
      <!--<button @click="increment()">Clicks: {{ state.count }} Double: {{ state.double }}</button>-->
      <ul>
        <li>Event 1</li>
        <li>Event 1</li>
        <li>Event 1</li>
        <li>Event 1</li>
        <li>Event 1</li>
        <li>Event 1</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { reactive, computed, onMounted, ref } from "vue";
import videojs from "video.js";

export default {
  /* eslint-disable no-console */
  setup() {
    const videoPlayerRef = ref();
    const h1ref = ref();
    let player = ref(null);
    const playerOptions = {
      autoplay: true,
      controls: true,
      fluid:true,
      responsive: true,
      sources: [
        {
          src:
            "https://cdn.jsdelivr.net/npm/big-buck-bunny-1080p@0.0.6/video.mp4",
          type: "video/mp4"
        }
      ]
    };
    const state = reactive({
      count: 0,
      double: computed(() => state.count * 2)
    });

    function increment() {
      state.count++;
    }

    onMounted(() => {
      console.log(h1ref);
      console.log(videoPlayerRef);
      player = videojs(
        videoPlayerRef.value,
        playerOptions,
        function onPlayerReady() {}
      );
    });

    return { state, increment, videoPlayerRef, player };
  }
};
</script>

<style scoped>
@import './../../node_modules/video.js/dist/video-js.css';
.course {
  display :flex;
  justify-content: space-around;
  align-items: stretch;
  align-content: center;
}

.player {
  width: 60vw;
}

.course-overview {
  background-color: honeydew;
}

</style>