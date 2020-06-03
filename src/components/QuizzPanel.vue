<template>
  <section>
    <div class="panel" v-if="!answer">
      <div class="head">
        <p>What is 💁🏽‍♂️ ({{num1}} {{opt}} {{num2}}) ?</p>
      </div>
      <div class="cards">
        <card v-for="(card, index) in cards" :key="index" :guess="guess" :answer="answer" :num="card"></card>
      </div>
    </div>
    <transition
      name="fade"
      >
      <div class="congrats-panel" animate__animated animate__rubberBand v-if="answer">
        <div class="info">
          <h1>Congratulations 🔥🕺🏼🔥</h1>
          <span>u got the right answer..</span><br><br>
          <button @click="next">Next Quizz</button>
        </div>
      </div>
    </transition>
  </section>
</template>

<script>
import Card from '@/components/Card.vue';

export default {
  name: 'QuizzPanel',
  components: {
    Card,
  },
  data: () => ({
    num1: 0,
    num2: 0,
    opt: '+',
    result: 0,
    cards: [],
    answer: false,
  }),
  mounted() {
    this.num1 = this.getRandomArbitrary(-30, 50);
    this.num2 = this.getRandomArbitrary(-20, 30);
    this.opt = this.getRandomOpt(10, 5);
    this.result = this.getResult();
    this.getCardsNumber(-30, 50);
    this.addResultToCards();

  },
  methods: {
    guess(num) {
      if (num === this.result) {
        this.answer = true;
      } else {
        this.answer = false;
      }
    },
    getRandomArbitrary(min, max) {
      return Math.floor(Math.random() * (max - min) + min);
    },
    getRandomOpt(min, max) {
      let num = this.getRandomArbitrary(min, max);
      if(num >= 1 && num <= 5) {
        return '-';
      }else {
        return '+';
      }
    },
    getResult() {
      if (this.opt === '+') {
        return this.num1 + this.num2
      }
      return this.num1 - this.num2;
    },
    getCardsNumber(min, max) {
      if(this.cards.length <= 3) {
        for(let i = 0; i < 3; i++) {
          this.cards.push(this.getRandomArbitrary(min, max));
        }
      }
    },
    addResultToCards() {
      let index = this.getRandomArbitrary(1, 4);
      this.cards.splice(index, 0, this.result);
    },
    next() {
      this.answer = !this.answer;
      // 
      this.cards = [];
      this.result = 0;
      this.num1 = 0;
      this.num2 = 0;
      this.opt = "";
      this.num1 = this.getRandomArbitrary(-30, 50);
      this.num2 = this.getRandomArbitrary(-20, 30);
      this.opt = this.getRandomOpt(10, 5);
      this.result = this.getResult();
      this.getCardsNumber(-30, 50);
      this.addResultToCards();
    },
  },
};
</script>

<style>
button {
  padding: 10px 20px;
  font-size: 1em;
  font-weight: bold;
  background-color: turquoise;
  border-radius: 10px;
  color: white;
  border: none;
}
.fade-enter {
  opacity: 0;
  transform: rotateY(360deg);
}
.fade-enter-active {
  transition: all 2s ease-out;
}

.animate__animated.animate__rubberBand {
  --animate-duration: 2s;
}
.panel, .congrats-panel {
  width: 500px;
  height: 300px;
  background: rgb(230, 230, 230);
  margin: 50px auto;
  box-shadow: 2px 2px 5px #ccc;
  border-radius: 10px;
}
.head {
  width: 100%;
  height: 35px;
  background-color: rgb(163, 163, 163);
  border-radius: 10px 10px 0px 0px;
}
.cards {
  display: grid;
  grid-template-columns: repeat(2, 100px);
  gap: 30px;
}
.congrats-panel {
  background-color: rgb(189, 245, 189);
  color: green;
  text-align: center;
  position: relative;
}
.congrats-panel h1 {
  font-weight: bold;
}
.info {
  position: absolute;
  top: 100px;
  left: 120px;
}
</style>
