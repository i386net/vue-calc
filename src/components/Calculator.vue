<template>
  <div class="container">
    <div class="calculator">

      <div class="calculator__display">
        <div class="calculator__icons">
          <div class="calculator__icon calculator__icon_cancel">×</div>
          <div class="calculator__icon calculator__icon_min"> −</div>
          <div class="calculator__icon calculator__icon_max">+</div>
        </div>
        {{ current || '0' }}

      </div>
      <div class="calculator__button calculator__button_special" @click="clear()">C</div>
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
      <div class="calculator__button zero calculator__button_number calculator__button_border_bl" @click="append('0')">0</div>
      <div class="calculator__button calculator__button_number" @click="dot">,</div>
      <div class="calculator__button calculator__button_operator calculator__button_border_br" @click="equal">=</div>
    </div>
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
      this.previous = '';
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
            parseFloat(this.previous),
            parseFloat(this.current)
        )
      }`;
      this.previous = null;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container {
    width: 100%;
    height: 100%;
    background-color: #2c3e50;
    display: flex;
    flex-direction: column;

  }
  .calculator {
    width: 300px;
    margin: auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    font-size: 40px;
    color: #ffffff;
    -webkit-box-shadow: -2px 10px 31px 0 rgba(0,0,0,0.75);
    -moz-box-shadow: -2px 10px 31px 0 rgba(0,0,0,0.75);
    box-shadow: -2px 10px 31px 0 rgba(0,0,0,0.75);
    border-radius: 5px;
  }
  .calculator__display {
    grid-column: 1/5;
    background-color: rgb(88, 92, 95);
    border-radius: 5px 5px 0 0;
    text-align: right;
    padding-right: 10px;
  }
  .zero {
    grid-column: 1 / 3;
  }
  .calculator__button {
    border: 1px solid rgb(88, 92, 95);
    cursor: pointer;
  }
  .calculator__button:active {
    background-color: rgb(182, 183, 184);
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
  .calculator__button_border_br {
    border-radius: 0 0 5px 0;
  }
  .calculator__button_border_bl {
    border-radius: 0 0 0 5px;
  }
  .calculator__icons {
    height: 18px;
    display: flex;
    flex-direction: row;
    font-size: 16px;
    color: transparent;
  }
  .calculator__icons:hover {
    color: black;
  }
  .calculator__icon {
    width: 12px;
    height: 12px;
    margin-top: 4px;
    margin-left: 4px;
    border-radius: 50%;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .calculator__icon_cancel {
    background-color: rgb(237, 101, 89);
  }
  .calculator__icon_min {
    background-color: rgb(224, 192, 76);
  }
  .calculator__icon_max {
    background-color: rgb(115, 190, 70);
  }
</style>
