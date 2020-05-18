<template>
    <div class="question-box-container">
         <b-jumbotron>
           <!-- <template v-slot:header>Header</template>-->

            <template v-slot:lead>
                <p v-html="quesAns.question"></p>
            </template>

            <hr class="my-4">
            <AnswerList :answersArr = "shuffledAnswers" :correctAns = "correctAns" v-on="$listeners"/>

            <b-button variant="success"  @click="next">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>

import AnswerList from '@/components/AnswerList.vue'
var _ = require('lodash');

export default {
    props: {
        quesAns: Object,
        next: Function
    },
    data() {
        return {
            shuffledAnswers: [],
            correctAns: ""
        }
    },
    components: {
        AnswerList
    },
    /*computed: {
        answers() {
             let answers = [...this.quesAns.incorrect_answers,this.quesAns.correct_answer];
             return answers;
        }
    },*/
    methods: {
        shuffleAnswers() {
            let answers = [...this.quesAns.incorrect_answers,this.quesAns.correct_answer];
            this.shuffledAnswers = _.shuffle(answers);
            this.correctAns = this.quesAns.correct_answer;
        }
    },
    watch: {
        quesAns: {
            immediate: true,
            handler() {
                 this.shuffleAnswers()
            }
        }
        /*What immediate does is instead of only running this watch function when quesAns updates, it also runs it when quesAns 
            passed as props and every subsequent time when it updates.
        */

        // quesAns() {
        //     this.shuffleAnswers()
        // }
    },
}
</script>


<style scoped>
    .btn{
        margin-top: 20px;
        color: white;
    }
</style>