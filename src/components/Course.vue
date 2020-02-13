<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">Farming</h5>
      <div class="player">
        <video ref="videoPlayerRef" class="video-js">
        </video>
      </div>
    </div>
    <div v-if="currentQuestion.answers" class="modal-absolute">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">{{currentQuestion.question}}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close" @click="resume">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <ul class="list-group">
              <li v-for="(answer,index) in currentQuestion.answers" v-bind:key="index" class="list-group-item">
                {{answer}} - test
              </li>
            </ul>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script>
  /* eslint-disable no-console */
  import { onMounted, ref } from "vue";
  import videojs from "video.js";
  import "videojs-markers-plugin";

  export default {
    props: {
      questions: Object
    },

    setup(props, context) {
      const videoPlayerRef = ref();
      let player = ref();

      let currentQuestion = ref({})

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
            "z-index":0,          
            "border-radius": "50%",
            "background-color": "orange"
          },
          markerTip: {
            display: false
          },
          breakOverlay: {
            display: false,
          },
          markers: getMarkers(props.questions),
          onMarkerReached: marker => {
            context.emit("markerReached", marker);
            
            currentQuestion.value = props.questions[marker.id];
            player.pause();

            /*let options = {};
            options.label = 'the label';

            var ModalDialog = videojs.getComponent('ModalDialog');
            var myModal = new ModalDialog(player, options);
            player.addChild(myModal);
            myModal.open();*/
          }
        });
      });

      const resume = () => {
        currentQuestion.value = {}
        player.play();
      }

      return { videoPlayerRef, player, resume, currentQuestion };
    }
  };

  function getMarkers(questions) {
    let markers = [];
    for (let [key, value] of Object.entries(questions)) {
      markers.push({
        time: value.time,
        overlayText: value.question,
        id: key
      });
    }
    return markers;
  }


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

  .modal-absolute{
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }

</style>