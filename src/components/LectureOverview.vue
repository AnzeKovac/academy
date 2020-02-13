<template>
    <div>
        <div class="list-group">
            <lecture-overview-item v-for="(question,index) in questions" v-bind:key="index" :question="question"></lecture-overview-item>
        </div>
    </div>

</template>

<script>
    import LectureOverviewItem from './LectureOverviewItem.vue';
    export default {
        props: {
            questions: Array
        },
        components: {
            LectureOverviewItem
        }
    }
</script>