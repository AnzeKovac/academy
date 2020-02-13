<template>
    <a href="#" class="list-group-item list-group-item-action flex-column align-items-start" v-bind:class="{active : question.active}">
        <div class="container">
            <div class="row">
                <div class="col-10">
                    <div class="d-flex w-100 justify-content-between">
                        <h5 class="mb-1">{{question.question}}</h5>
                    </div>
                    <p class="mb-1">{{question.description}}</p>
                    <div class="progress">
                        <div class="progress-bar bg-info" v-bind:style="{width:progress+'%'}" role="progressbar" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100"></div>
                      </div>
                </div>
                <div class="col-2">
                    <h2 v-if="progress > 75">✔</h2>
                </div>
            </div>
        </div>

    </a>
</template>

<script>
    /* eslint-disable no-console */
    import {watch,ref} from 'vue'; 
    export default {
        props: {
            question: Object
        },
        setup(props){
            let progress = ref(0);
            watch(() => props.question.score, () => {
                progress.value = Math.round((100 * props.question.score) / props.question.points);
            })

            return {progress};
        }
    }
</script>