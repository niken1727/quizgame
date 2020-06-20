<template>
    <div class="question-box-container">
        <b-jumbotron>
            <template v-slot:lead>
                {{ currentQuestion.question }}
            </template>

            <hr class="my-4">
            <b-list-group >
                <b-list-group-item v-for="(answer,index) in shuffledAnswers" :key="index" 
            @click="selectAnswer(index)"
            :class="[selectedIndex == index ? 'selected' : '']"> 
                       {{ answer }}
                </b-list-group-item>
            </b-list-group>
        

            <b-button variant="primary"
                @click="this.submitAnswer">
                           Submit
            </b-button>
            <b-button @click="next" variant="success" href="#">Next</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
import _ from 'lodash'

export default {
    props: {
        currentQuestion: Object,
        next: Function,
        increment: Function
    },
    data: function() {
        return {
            correctIndex: null,
            selectedIndex: null,
            shuffledAnswers: []
        }
    },
    computed:{
        answers(){
            let answers = [...this.currentQuestion.incorrect_answers]
            answers.push(this.currentQuestion.correct_answer)
            return answers
        }
    },
    watch: {
        currentQuestion: {
            immediate : true,
            handler(){
                this.selectedIndex = null
                this.shuffleAnswers()
            }
        }
    },
    methods: {
        selectAnswer(index){
            console.log(index)
            this.selectedIndex = index
        },
        submitAnswer(){
            let isCorrect = false;
                console.log("correcti", this.selectedIndex)
                console.log("correctv", this.correctIndex)

            if(this.selectedIndex == this.correctIndex){
                isCorrect = true
                console.log("correct", this.isCorrect)
            }
            this.increment(isCorrect)
        },
        shuffleAnswers(){
            let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
            this.shuffledAnswers = _.shuffle(answers)
            this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
            console.log("correct index",this.correctIndex)
        }
    }
}
</script>

<style scoped>
    .list-group {
        margin-bottom: 15px;
    }

    .list-group-item:hover {
        background: #EEE;
        cursor: pointer;
    }

    .btn {
        margin: 0 5px;
    }

    .selected {
        background-color: lightblue;
    }

    .correct {
        background-color: lightgreen;
    }

    .incorrect {
        background-color: red;
    }
</style>