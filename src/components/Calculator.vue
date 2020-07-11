<template>
  <div class="calculator">
    <div class="calculator__display">{{ current || '0' }}</div>
    <div class="calculator__button calculator__button_special" @click="clear">AC</div>
    <div class="calculator__button calculator__button_special" @click="sign">+/-</div>
    <div class="calculator__button calculator__button_special" @click="percent">%</div>
    <div class="calculator__button calculator__button_operator" @click="divide">÷</div>
    <div class="calculator__button calculator__button_number" @click="append('7')">7</div>
    <div class="calculator__button calculator__button_number" @click="append('8')">8</div>
    <div class="calculator__button calculator__button_number" @click="append('9')">9</div>
    <div class="calculator__button calculator__button_operator" @click="multiply">×</div>
    <div class="calculator__button calculator__button_number" @click="append('4')">4</div>
    <div class="calculator__button calculator__button_number" @click="append('5')">5</div>
    <div class="calculator__button calculator__button_number" @click="append('6')">6</div>
    <div class="calculator__button calculator__button_operator" @click="minus">−</div>
    <div class="calculator__button calculator__button_number" @click="append('1')">1</div>
    <div class="calculator__button calculator__button_number" @click="append('2')">2</div>
    <div class="calculator__button calculator__button_number" @click="append('3')">3</div>
    <div class="calculator__button calculator__button_operator" @click="plus">+</div>
    <div class="calculator__button zero calculator__button_number" @click="append('0')">0</div>
    <div class="calculator__button calculator__button_number" @click="dot">,</div>
    <div class="calculator__button calculator__button_operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current += number //`${this.current}${number}`
    },
    dot() {
      if( this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply(){
     this.operator = (a, b) => a * b;
     this.setPrevious();
    },
    minus() {
     this.operator = (a, b) => a - b;
     this.setPrevious();
    },
    plus() {
     this.operator = (a, b) => a + b;
     this.setPrevious();
    },
    equal() {
      this.current = `${
        this.operator(
            parseFloat(this.current),
            parseFloat(this.previous)
        )
      }`;
      this.previous = null;
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
