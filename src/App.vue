<template>
  <div class="app">
    <Display
      :inGame="inGame"
      :missCounter="missCounter"
      :restartCounter="restartCounter"
      :restartGame="restartGame"
    />
    <Board
      :cards="cards || []"
      :isWaiting="isWaiting"
      :openCard="openCard"
      :isEnd="isEnd"
    />
  </div>
</template>

  <script>
  import Display from './components/Display.vue';
  import Board from './components/Board.vue';

  export default {
    name: 'App',
    components: {
      Display,
      Board
    },
    data: () => ({
      cards: null,
      isWaiting: [],
      isFixed: true,
      isEnd: false,
      inGame: false,
      missCounter: 0,
      restartCounter: 0
    }),
    created() {
      this.generateCards();
    },
    methods: {
      generateCards() {
        this.isFixed = true;

        let a = [
          'https://image.flaticon.com/icons/svg/139/139093.svg',
          'https://image.flaticon.com/icons/svg/138/138957.svg',
          'https://image.flaticon.com/icons/svg/138/138811.svg',
          'https://image.flaticon.com/icons/svg/148/148845.svg',
          'https://image.flaticon.com/icons/svg/138/138281.svg',
          'https://image.flaticon.com/icons/svg/148/148717.svg',
          'https://image.flaticon.com/icons/svg/148/148908.svg',
          'https://image.flaticon.com/icons/svg/138/138935.svg'
        ],
        b = () => Math.floor(Math.random() * a.length),
        c = [],
        d = a.length * 2;
        
        a = [...a, ...a];
        for(let ma = 0; ma < d; ma++) { // shuffle
          let e = b();

          c.push({
            icon: a[e],
            isDone: false,
            id: ma
          });
          a.splice(e, 1);
        }

        return(
          this.cards = c,
          this.isFixed = false,
          this.inGame = true
        );
      },
      openCard(id, icon) {
        if(this.isFixed) return;
        
        if(!this.isWaiting.length) {
          this.isWaiting = [{
            icon,
            id
          }];
        } else {
          if(this.isWaiting[0].id === id) return;
          let a = this.isWaiting[0].icon === icon; // Same pair
          
          this.isWaiting.push({
            icon,
            id
          });

          if(!a) { // miss
            // fix array
            this.isFixed = true;

            // set timeout => clear this.isWaiting
            this.missCounter++;

            setTimeout(() => {
              this.isWaiting = [];
              this.isFixed = false;
            }, 500);
          } else {
            // fix active cards
            for(let ma = 0; ma < 2; ma++) { // Faster than filter.forEach
              this.cards.find(io => io.id === [this.isWaiting[0].id, id][ma]).isDone = true;
            }

            // clear this.isWaiting
            this.isWaiting = [];

            // The end?
            if(!this.cards.filter(io => io.isDone === false).length) {
              this.isFixed = true;
              this.inGame = false;

              setTimeout(() => {
                this.isEnd = true;
                this.cards = [];
              }, 750);
            }
          }
        }
      },
      restartGame() {
        this.cards = null;
        this.isWaiting = [];
        this.isFixed = true;
        this.isEnd = false;
        this.inGame = false;
        this.missCounter = 0;

        this.generateCards();

        this.restartCounter++;
      }
    }
  }
</script>

<style>
  @import './styles/App.css';
</style>

