<template>
    <div>
        <b-list-group>
            <b-list-group-item button :disabled="checkBool(selectedIndex)" v-for="(answer,index) in answersArr" :key="index" @click="selectIndex(index)"
                :class = "[selectedIndex === index ? index == correctIndex ? 'correct' : 'incorrect' : index == correctIndex ? 'correct' : '']">
                {{answer}}
            </b-list-group-item>
        </b-list-group>
    </div>
</template>


<script>
export default {
    props: [
        'answersArr',
        'correctAns' 
    ],
    data() {
        return {
            selectedIndex: null,
                    correctIndex: null
        }
    },
    computed: {
       
    },
    methods: {
        selectIndex(index) {
            this.selectedIndex = index;
            this.correctIndex = this.answersArr.indexOf(this.correctAns);
            this.$emit('inc-attempted');
            if(this.answersArr[index] == this.correctAns) {
                this.$emit('inc-value');
            }
        },
         checkBool(selIndex) {
            return selIndex || selIndex === 0? true : false;
        }
    },
    watch: {
        answersArr() {
            this.selectedIndex = null;
            this.correctIndex = null;
        }
    },
}
</script>


<style scoped>
    .list-group {
        margin-bottom: 20px;
    }
    @media (hover: hover) {
        .list-group-item:hover {
            background-color: #ccc;
            cursor: pointer;
        }
    }

    .correct {
        background-color: lightgreen;
        color:black;
        font-weight: bold;
    }

    .incorrect {
        background-color: tomato;
        color:white;
        font-weight: bold;
    }
</style>

