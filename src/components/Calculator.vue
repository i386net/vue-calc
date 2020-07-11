<template>
  <div class="calculator">
    <div class="calculator__display">{{ current || '0' }}</div>
    <div class="calculator__button calculator__button_special" @click="clear">AC</div>
    <div class="calculator__button calculator__button_special" @click="sign">+/-</div>
    <div class="calculator__button calculator__button_special">%</div>
    <div class="calculator__button calculator__button_operator">÷</div>
    <div class="calculator__button calculator__button_number">7</div>
    <div class="calculator__button calculator__button_number">8</div>
    <div class="calculator__button calculator__button_number">9</div>
    <div class="calculator__button calculator__button_operator">×</div>
    <div class="calculator__button calculator__button_number">4</div>
    <div class="calculator__button calculator__button_number">5</div>
    <div class="calculator__button calculator__button_number">6</div>
    <div class="calculator__button calculator__button_operator">−</div>
    <div class="calculator__button calculator__button_number">1</div>
    <div class="calculator__button calculator__button_number">2</div>
    <div class="calculator__button calculator__button_number">3</div>
    <div class="calculator__button calculator__button_operator">+</div>
    <div class="calculator__button zero calculator__button_number">0</div>
    <div class="calculator__button calculator__button_number">,</div>
    <div class="calculator__button calculator__button_operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .calculator {
    width: 400px;
    margin: auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    font-size: 40px;
    color: #ffffff;
  }
  .calculator__display {
    grid-column: 1/5;
    background-color: rgb(88, 92, 95);
  }
  .zero {
    grid-column: 1 / 3;
  }
  .calculator__button {
    border: 1px solid rgb(88, 92, 95);
  }
  .calculator__button_operator {
    background-color: darkorange;
  }
  .calculator__button_number {
    background-color: rgb(129, 131, 133);
  }
  .calculator__button_special {
    background-color: rgb(104, 107, 110);
  }
</style>
