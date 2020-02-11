<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">Farming 101</h5>
      <div class="player">
        <video ref="videoPlayerRef" class="video-js"></video>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, computed, onMounted, ref } from "vue";
import videojs from "video.js";
import 'videojs-markers-plugin';

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

      player.markers({
        markerStyle: {
           'width':'5px',
           'border-radius': '40%',
           'background-color': 'orange'
        },
        markerTip:{
           display: true,
           text: function(marker) {
              return "I am a marker tip: "+ marker.text;
           }
        },
        breakOverlay:{
           display: true,
           displayTime: 4,
           style:{
              'width':'100%',
              'height': '10%',
              'background-color': 'rgba(10,10,10,0.6)',
              'color': 'white',
              'font-size': '16px'
           },
           text: function(marker) {
              return "This is a break overlay: " + marker.overlayText;
           },
        },
        markers: [
           {time: 9.5, text: "this", overlayText: "1", class: "special-blue"},
           {time: 16,  text: "is", overlayText: "2"},
           {time: 23.6,text: "so", overlayText: "3"},
           {time: 28,  text: "cool", overlayText: "4"}
        ],
        onMarkerReached: () => {
          player.pause();
        }   
     });
    });

    return { state, increment, videoPlayerRef, player };
  }
};
</script>

<style scoped>
@import './../../node_modules/video.js/dist/video-js.css';
@import './../../node_modules/videojs-markers-plugin/dist/videojs.markers.plugin.css';
/* hide time display on progress bar on the mouse position */
.video-js .vjs-progress-control:hover .vjs-mouse-display,
/* hide time display on progress bar on the current play position */
.video-js .vjs-progress-holder .vjs-play-progress {
   display: none; 
}
</style>