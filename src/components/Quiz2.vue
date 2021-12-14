<template>
    <div class="container-fluid">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h3>Q. Mudou de componente?</h3>
                </div>
                <div class="modal-body">
                    <div class="col-xs-3 5"> </div>
                    <div class="quiz" id="quiz" data-toggle="buttons">
                        <div class="row"> 
                            <label class="element-animation1 btn btn-lg btn-danger btn-block">
                                <span class="btn-label"><i class="glyphicon glyphicon-chevron-right"></i></span> 
                                <input type="radio" name="q_answer" value="Sim" id="q_answer1" v-model="picked" @change="onSubmit()"> Sim
                            </label> 
                        </div>
                        <div class="row mt-2"> 
                            <label class="element-animation2 btn btn-lg btn-danger btn-block">
                                <span class="btn-label"><i class="glyphicon glyphicon-chevron-right"></i></span> 
                                <input type="radio" name="q_answer" value="Não" id="q_answer2" v-model="picked" @change="onSubmit()"> Não
                            </label> 
                        </div>
                        <div class="row mt-2">
                            <label class="element-animation3 btn btn-lg btn-danger btn-block">
                                <span class="btn-label"><i class="glyphicon glyphicon-chevron-right"></i></span>
                                <input type="radio" name="q_answer" value="Talvez" id="q_answer3" v-model="picked" @change="onSubmit()"> Talvez
                            </label>
                        </div>
                        <div class="row mt-2">
                            <label class="element-animation4 btn btn-lg btn-danger btn-block">
                                <span class="btn-label"><i class="glyphicon glyphicon-chevron-right"></i></span> 
                                <input type="radio" name="q_answer" value="Não sei" id="q_answer4" v-model="picked" @change="onSubmit()"> Não sei 
                            </label>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { Options, Vue } from 'vue-class-component';

    @Options({})
    export default class Quiz2 extends Vue {
        picked = "";

        onSubmit(){
            this.$emit('send-answer', this.picked)
        }
    }
</script>

<style scoped>
    input[type="radio"]{
        visibility:hidden;
    }

    label.btn {
        padding: 18px 60px;
        white-space: normal;
        -webkit-transform: scale(1.0);
        -moz-transform: scale(1.0);
        -o-transform: scale(1.0);
        -webkit-transition-duration: .3s;
        -moz-transition-duration: .3s;
        -o-transition-duration: .3s
    }

    label.btn:hover {
        text-shadow: 0 3px 2px rgba(0, 0, 0, 0.4);
        -webkit-transform: scale(1.1);
        -moz-transform: scale(1.1);
        -o-transform: scale(1.1)
    }

    label.btn-block {
        text-align: left;
        position: relative
    }

    label .btn-label {
        position: absolute;
        left: 0;
        top: 0;
        display: inline-block;
        padding: 0 10px;
        background: #000000;
        height: 100%
    }

    label .glyphicon {
        top: 34%
    }

    .element-animation1 {
        animation: animationFrames ease .8s;
        animation-iteration-count: 1;
        transform-origin: 50% 50%;
        -webkit-animation: animationFrames ease .8s;
        -webkit-animation-iteration-count: 1;
        -webkit-transform-origin: 50% 50%;
        -ms-animation: animationFrames ease .8s;
        -ms-animation-iteration-count: 1;
        -ms-transform-origin: 50% 50%
    }

    .element-animation2 {
        animation: animationFrames ease 1s;
        animation-iteration-count: 1;
        transform-origin: 50% 50%;
        -webkit-animation: animationFrames ease 1s;
        -webkit-animation-iteration-count: 1;
        -webkit-transform-origin: 50% 50%;
        -ms-animation: animationFrames ease 1s;
        -ms-animation-iteration-count: 1;
        -ms-transform-origin: 50% 50%
    }

    .element-animation3 {
        animation: animationFrames ease 1.2s;
        animation-iteration-count: 1;
        transform-origin: 50% 50%;
        -webkit-animation: animationFrames ease 1.2s;
        -webkit-animation-iteration-count: 1;
        -webkit-transform-origin: 50% 50%;
        -ms-animation: animationFrames ease 1.2s;
        -ms-animation-iteration-count: 1;
        -ms-transform-origin: 50% 50%
    }

    .element-animation4 {
        animation: animationFrames ease 1.4s;
        animation-iteration-count: 1;
        transform-origin: 50% 50%;
        -webkit-animation: animationFrames ease 1.4s;
        -webkit-animation-iteration-count: 1;
        -webkit-transform-origin: 50% 50%;
        -ms-animation: animationFrames ease 1.4s;
        -ms-animation-iteration-count: 1;
        -ms-transform-origin: 50% 50%
    }

    @keyframes animationFrames {
        0% {
            opacity: 0;
            transform: translate(-1500px, 0px)
        }

        60% {
            opacity: 1;
            transform: translate(30px, 0px)
        }

        80% {
            transform: translate(-10px, 0px)
        }

        100% {
            opacity: 1;
            transform: translate(0px, 0px)
        }
    }

    @-webkit-keyframes animationFrames {
        0% {
            opacity: 0;
            -webkit-transform: translate(-1500px, 0px)
        }

        60% {
            opacity: 1;
            -webkit-transform: translate(30px, 0px)
        }

        80% {
            -webkit-transform: translate(-10px, 0px)
        }

        100% {
            opacity: 1;
            -webkit-transform: translate(0px, 0px)
        }
    }

    .modal-header {
        background-color: transparent;
        color: inherit
    }

    .modal-body {
        min-height: 300px
    }
</style>