<template>
    <div :class="`display-card${( (!isOpened && !isDone) ? '' : ' rotated' ) + ( (!isDone) ? '' : ' hidden' )}`" @click="handleChoose">
        <div class="display-card-front display-card-side"></div>
        <div class="display-card-back display-card-side">
            <img class="display-card-back-icon" :src="icon" :alt="id" />
        </div>
    </div>
</template>

<script>
    export default {
        name: "Card",
        props: {
            id: {
                type: Number,
                default: -1
            },
            icon: {
                type: String,
                default: ""
            },
            isOpened: {
                type: Boolean,
                default: false
            },
            isDone: {
                type: Boolean,
                default: false
            },
            handleChoose: {
                type: Function,
                default: () => null
            }
        }
    }
</script>

<style>
    @import '../styles/Card';
</style>
