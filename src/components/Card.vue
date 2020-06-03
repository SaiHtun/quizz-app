<template>
  <div class="card animate__animated" :class="{falseBg: click || answer, animate__shakeX: click || answer}">
    <span class="animate__animated" :class="{animate__shakeY: click || answer}" @click="submit">{{num}}</span>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: ['num', 'answer', 'guess'],
  data: () => ({
    click: false,
  }),
  methods: {
    submit() {
      this.guess(this.num);
      this.click = true;
    },
  }
};
</script>

<style>
.card {
  width: 50px;
  height: 50px;
  text-align: center;
  line-height: 50px;
  background-color: skyblue;
  border-radius: 10px;
  margin-left: 150px;
  margin-top: 35px;
  cursor: pointer;
}
.falseBg {
  background-color: red;
}
</style>
