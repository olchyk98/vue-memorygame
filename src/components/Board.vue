<template>
    <div :class="`board it empty ${ (!isEnd) ? '' : ' done' }`">
        <Card
            v-for="{ id, icon, isDone } in cards"
            v-if="!isEnd"
            :key="id"
            :icon="icon"
            :isOpened="Boolean(isWaiting.find(io => io.id === id))"
            :isDone="isDone"
            :handleChoose="() => openCard(id, icon)"
        />
        <span class="board-end" v-if="isEnd">Great Job!</span>
        <!-- v-else is dead -->
    </div>
</template>

<script>
    import Card from './Card.vue';

    export default {
        name: "Board",
        components: {
            Card
        },
        props: {
            cards: {
                type: Array,
                default: []
            },
            openCard: {
                type: Function,
                default: () => null
            },
            isWaiting: {
                type: Array,
                default: []
            },
            isEnd: {
                type: Boolean,
                default: false
            }
        }
    }
</script>

<style>
    @import '../styles/Board.css';
</style>

