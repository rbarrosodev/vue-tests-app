<template>
    <component id="quizbox" style="margin-top: 100px;" v-bind:is="component" @send-answer="toggle"/>
</template>

<script lang="ts">
    import { Options, Vue } from 'vue-class-component';
    import Quiz from './Quiz.vue';
    import Quiz2 from './Quiz2.vue';
    import QuizCompleted from './QuizCompleted.vue'

    interface QuizData {
        answer: string;
    }   

    @Options({
        components: {
            Quiz,
            Quiz2,
            QuizCompleted,
        },
    })
    export default class QuizParent extends Vue {
        component = "Quiz";
        str = "";
        answers: QuizData[] = [];
        i = 0;

        toggle(param: QuizData){
            this.answers.push(param);
            console.log(this.answers);

            if (this.component == "Quiz") { 
                this.component = "Quiz2";
            } else if (this.component == "Quiz2") {
                this.axios.post(`http://localhost:3000/questions.json`, {
                    answer1: this.answers[0],
                    answer2: this.answers[1]
                });

                this.component = "QuizCompleted";
                setTimeout(() => { 
                    document.getElementById('quizbox').remove()                  
                 }, 3000);
            }
        }
    }
</script>