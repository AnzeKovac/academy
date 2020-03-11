<template>
  <div class="card">
    <div class="card-body">
      <div class="player">
        <video ref="videoPlayerRef" class="video-js"></video>
      </div>
    </div>
    <question-dialog :currentQuestion="currentQuestion"/>
    tralalal
  </div>
</template>

<script>
/* eslint-disable no-console */
import { onMounted, ref } from "vue";
import QuestionDialog from './QuestionDialog.vue';
import videojs from "video.js";
import "videojs-markers-plugin";

export default {
  props: {
    questions: Object
  },
  componennts : {
    QuestionDialog
  },
  setup(props, context) {
    const videoPlayerRef = ref();
    let player = ref();

    let currentQuestion = ref({});

    const playerOptions = {
      autoplay: true,
      controls: true,
      fluid: true,
      responsive: true,
      sources: [
        {
          src:
            "https://cdn.jsdelivr.net/npm/big-buck-bunny-1080p@0.0.6/video.mp4",
          type: "video/mp4"
        }
      ]
    };

    onMounted(() => {
      player = videojs(
        videoPlayerRef.value,
        playerOptions,
        function onPlayerReady() {
          player.controlBar.progressControl.disable();
        }
      );

      player.markers({
        markerStyle: {
          width: "4px",
          "z-index": 0,
          "border-radius": "50%",
          "background-color": "orange"
        },
        markerTip: {
          display: false
        },
        breakOverlay: {
          display: false
        },
        markers: getMarkers(props.questions),
        onMarkerReached: marker => {
          context.emit("markerReached", marker);

          currentQuestion.value = props.questions[marker.id];
          player.addClass("blur");
          player.removeClass("no-blur");
          player.pause();
        }
      });
    });

    const resume = () => {
      currentQuestion.value = {};
      player.removeClass("blur");
      player.addClass("no-blur");
      player.play();
    };

    return { videoPlayerRef, player, resume, currentQuestion };
  }
};

const getMarkers = questions => {
  let markers = [];
  for (let [key, value] of Object.entries(questions)) {
    markers.push({
      time: value.time,
      overlayText: value.question,
      id: key
    });
  }
  return markers;
};
</script>

<style scoped>
@import "./../../node_modules/video.js/dist/video-js.css";
@import "./../../node_modules/videojs-markers-plugin/dist/videojs.markers.plugin.css";

/* hide time display on progress bar on the mouse position */
.video-js .vjs-progress-control:hover .vjs-mouse-display,
  /* hide time display on progress bar on the current play position */
  .video-js .vjs-progress-holder .vjs-play-progress {
  display: none;
}
.no-blur {
  filter: blur(0px);
  transition: 0.5s filter linear;
}

.blur {
  filter: blur(5px);
  transition: 0.25s filter linear;
}

.answer:hover {
  background-color: rgba(250, 250, 250, 1);
  cursor:pointer;
}
</style>