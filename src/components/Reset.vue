<template>
    <div>
        <b-jumbotron>
            <p> Total Questions: {{numOfTotal}} </p>
            <p> Attempted: {{attempted}} </p>
            <p> Correct Answers: {{numOfCorrect}} </p>
            <p> Wrong Answers: {{wrong}} </p>
            <h1>Answer New Questions Every Time...</h1>
            <b-button variant="success" @click="callInit">Start</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
export default {
    props: {
        callInit: Function,
        numOfCorrect: Number,
        numOfTotal: Number,
        attempted: Number
    },
    computed: {
        wrong() {
            return this.attempted - this.numOfCorrect;
        }
    }
}
</script>

<style scoped>
    p {
        font-size: 25px;
        font-weight: bold;
    }

    p,h1 {
        color: white;
    }

    .btn{
        margin-top: 20px;   
    }
</style>
