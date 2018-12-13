<template>
    <div class="display it">
        <span>Time: {{ time | convertTime }}</span>
        <button class="display-restart" @click="restartGame">Reset</button>
        <span>Miss: {{ missCounter }}</span>
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
            },
            restartGame: {
                type: Function,
                default: () => null
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
                    this.time++;
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
            convertTime(a) {
                a = parseInt(a);

                let b = b => Math.floor(b),
                    c = b(a / 60),
                    d = b(a % 60),
                    e = e => (e.toString().length === 1) ? '0' + e : e;

                return `${ e(c) }:${ e(d) }`;
            }
        },
        watch: {
            inGame(a) {
                if(a) this.startTimer();
                this.stopTimer();
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

