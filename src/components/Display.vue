<template>
    <div class="display it">
        <div class="display-front display-side">
            <span>Time: {{ time | convertTime }}</span>
            <span>Miss: {{ missCounter }}</span>
        </div>
        <div class="display-back display-side">
            <span>Hello :)</span>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Display",
        props: {
            inGame: {
                type: Boolean,
                default: false
            },
            missCounter: {
                type: Number,
                default: 0
            },
            restartCounter: {
                type: Number,
                default: 0
            }
        },
        created() {
            this.startTimer();
        },
        data: () => ({
            time: 0,
            timer: null
        }),
        methods: {
            startTimer() {
                clearInterval(this.timer);
                this.timer = setInterval(() => {

                }, 1000);
            },
            stopTimer() {
                clearInterval(this.timer);
            },
            resetTimer() {
                this.time = 0;
                this.startTimer();
            }
        },
        filters: {
            convertTime() {

            }
        },
        watch: {
            inGame(a) {
                if(a) this.startTimer();
                this.stopCounter();
            },
            restartCounter(a, b) {
                if(a > b) { // restart
                    this.resetTimer();
                }
            }
        }
    }
</script>

<style>
    @import '../styles/Display.css';
</style>

