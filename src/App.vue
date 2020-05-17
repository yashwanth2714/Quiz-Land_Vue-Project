<template>
  <div id="app">
    <Header :numOfCorrect = "numOfCorrect" :numOfTotal = "numOfTotal" :attempted = "numOfAttempted" :quizOver = "quizOver" />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="12" >
          <QuestionBox v-if="quesAnsArr.length && index < quesAnsArr.length" :quesAns = "quesAnsArr[index]" :next="next" @inc-value="increment" @inc-attempted="incrAttempted"/>
          <!-- We are not redendering question box untill we get data from API. So, here we are checking the array length
          If it's length is > 0 it wiil return true and questionvox will be rendered otherwise not rendered without the data  -->
        </b-col>
        <b-col sm="12" >
          <Reset v-if=" quesAnsArr.length && index === quesAnsArr.length" :callInit ="init" :numOfCorrect = "numOfCorrect" :numOfTotal = "numOfTotal" :attempted = "numOfAttempted"/>
        </b-col>
        <b-col sm="12" >
          <img :src="loadingSvg" v-if="!quesAnsArr.length" /> 
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import Reset from './components/Reset.vue'


export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Reset
  },
  data() {
    return {
      quesAnsArr: [],
      index: 0,
      numOfCorrect: 0,
      numOfTotal: 0,
      numOfAttempted: 0,
      quizOver: false,
      loadingSvg: require('./assets/loading2.svg')
    }
  },
  methods: {
    next() {
      this.index++;
      if(this.index === this.numOfTotal) {
        this.quizOver = true;
      }
    },
    increment() {
      this.numOfCorrect++;
    },
    incrAttempted() {
      this.numOfAttempted++;
    },
    init() {
      fetch("https://opentdb.com/api.php?amount=10&type=multiple")
        .then(response =>  response.json())
        .then(data => {
          this.quesAnsArr = data.results;
          this.numOfTotal = this.quesAnsArr.length;
          //reset the data properties after every API call
          this.index = 0;
          this.numOfCorrect= 0;
          this.numOfAttempted= 0;
          this.quizOver = false
        })
        .catch(err => console.log(err.message));
    }
  },
  mounted() {
      this.init()
    }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0px;
}

.bv-example-row {
  margin-top: 100px
}

.jumbotron {
  background-color: rgba(49, 46, 46, 0.733);
}

.lead {
  color: white;
}

</style>
