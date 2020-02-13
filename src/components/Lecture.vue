<template>
    <div class="container p-3">
        <div class="row">
            <div class="col-12">
                <course :questions="questions" @markerReached=handleMarkerReached></course>
            </div>
            <div class="col-12 p-3">
                <lecture-overview :questions="questions"></lecture-overview>
            </div>
        </div>
    </div>
</template>

<script>
    /* eslint-disable no-console */
    import { reactive } from "vue";
    import Course from './Course.vue'
    import LectureOverview from './LectureOverview.vue'

    export default {
        components: {
            Course,
            LectureOverview
        },
        setup() {
            const questions = reactive({
                cow_question:{
                    question: "How do you feed a cow",
                    description:"Learn what a cow eats",
                    answers: ["With milk", "Give it grass", "Don't feed it"],
                    points: 40,
                    score:0,
                    time: 5,
                    active:false,
                },
                tractor_question:{
                    question: "How do you drive a tracor",
                    description:"Want to know how to control 200hp+ machine ?",
                    answers: ["It's hard", "Pedal to the metal", "With caution"],
                    points: 20,
                    score:0,
                    time: 10,
                    active:false,
                },
                nature_question:{
                    question: "How do you survive in nature",
                    description: "Ask Bear.",
                    answers: ["Find nearest pizza place", "Call Bear", "Lay down and cry"],
                    points: 20,
                    score:0,
                    time: 15,
                    active:false,
                }
            });

            let currentlyActiveQuestionId = reactive();

            function handleMarkerReached(marker){
                //First clear previous question of active status
                if(currentlyActiveQuestionId){
                    questions[currentlyActiveQuestionId].active = false;
                }

                if(marker.id in questions){
                    questions[marker.id].active = true;
                    questions[marker.id].score = questions[marker.id].points-(Math.random()*10).toFixed(0);
                    currentlyActiveQuestionId = marker.id;
                }
            }

            return {
                questions,handleMarkerReached,currentlyActiveQuestionId
            }
        }
    };
</script>