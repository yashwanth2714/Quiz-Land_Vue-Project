<template>
    <div>
        <b-nav tabs fill class="bg">
            <b-nav-item disabled><h1><b>Quiz Land</b></h1></b-nav-item>
        </b-nav>
         <b-nav tabs fill>
            <b-nav-item disabled v-show="!quizOver" :class="{'total': !quizOver}"><b>Total Questions: {{numOfTotal}}</b></b-nav-item>
            <b-nav-item disabled v-show="!quizOver" :class="{'attempted': !quizOver}"><b>Attempted : {{attempted}}</b></b-nav-item>
            <b-nav-item disabled v-show="!quizOver" :class="{'correct': !quizOver}"><b>Correct: {{numOfCorrect}}</b></b-nav-item>
         </b-nav>
    </div>
</template>

<script>
export default {
    props: ['numOfCorrect', 'numOfTotal','attempted','quizOver']
}
</script>

<style scoped>
    .total {
        background-color: saddlebrown;
    }
    .attempted {
        background-color: darkorange;
    }
    .correct {
        background-color: darkgreen;
    }
    .bg {
        padding: 20px;
        background: #fc00ff;  /* fallback for old browsers */
        background: -webkit-linear-gradient(to right, #00dbde, #fc00ff);  /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(to right, #00dbde, #fc00ff); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
    }
    b {
        color: white;
    }
</style>
