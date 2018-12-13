<template>
    <div class="display it">
        <div class="display-front display-side">
            <span>Time: </span>
            <span>Miss: </span>
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
            }
        },
        data: () => ({
            time: 0
        }),
        methods: {
            startTimer() {
                
            }
        }
        created() {
            this.startTimer();
        },
        updated() {
            console.log("A");
        }
    }
</script>

<style>
    @import '../styles/Display.css';
</style>

