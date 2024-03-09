<template>
  <div class="calculator">
    <div class="display">{{ currentValue }}</div>
    <div class="buttons">
      
      <div @click="clear" class="button">C</div>
      <div @click="sign" class="button">+/-</div>
      <div @click="percent" class="button">%</div>
      <div @click="chooseOperator('÷')" class="button operator">÷</div>
      <div @click="appendNumber('7')" class="button">7</div>
      <div @click="appendNumber('8')" class="button">8</div>
      <div @click="appendNumber('9')" class="button">9</div>
      <div @click="chooseOperator('x')" class="button operator">x</div>
      <div @click="appendNumber('4')" class="button">4</div>
      <div @click="appendNumber('5')" class="button">5</div>
      <div @click="appendNumber('6')" class="button">6</div>
      <div @click="chooseOperator('-')" class="button operator">-</div>
      <div @click="appendNumber('1')" class="button">1</div>
      <div @click="appendNumber('2')" class="button">2</div>
      <div @click="appendNumber('3')" class="button">3</div>
      <div @click="chooseOperator('+')" class="button operator">+</div>
      <div @click="appendNumber('0')" class="button zero">0</div>
      <div @click="appendDecimal" class="button">.</div>
      <div @click="calculate" class="button operator"> = </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentValue: '',
      previousValue: null,
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.currentValue = '';
      this.previousValue = null;
      this.operator = null;
      this.operatorClicked = false;
    },
    sign() {
      this.currentValue = this.currentValue.charAt(0) === '-'
        ? this.currentValue.slice(1)
        : `-${this.currentValue}`;
    },
    percent() {
      this.currentValue = `${parseFloat(this.currentValue) / 100}`;
    },
    appendNumber(number) {
      if (this.operatorClicked) {
        this.currentValue = '';
        this.operatorClicked = false;
      }
      this.currentValue = `${this.currentValue}${number}`;
    },
    appendDecimal() {
      if (this.currentValue.indexOf('.') === -1) {
        this.currentValue += '.';
      }
    },
    chooseOperator(op) {
      if (this.currentValue === '') return;
      if (this.previousValue !== null) this.calculate();
      this.operator = op;
      this.previousValue = this.currentValue;
      this.operatorClicked = true;
    },
    calculate() {
      if (this.previousValue === null || this.currentValue === '') return;
      let calculation = parseFloat(this.previousValue);
      const current = parseFloat(this.currentValue);
      switch (this.operator) {
        case '+':
          calculation += current;
          break;
        case '-':
          calculation -= current;
          break;
        case 'x':
          calculation *= current;
          break;
        case '÷':
          if (current === 0) {
            this.currentValue = 'Error';
            return;
          }
          calculation /= current;
          break;
        default:
          return;
      }
      this.currentValue = calculation;
      this.operator = null;
      this.previousValue = null;
      this.operatorClicked = false;
    },
  },
};
</script>

<style scoped>
.calculator {
  max-width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.display {
  font-size: 24px;
  padding: 10px;
  margin-bottom: 15px;
  text-align: right;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}

.button {
  font-size: 20px;
  padding: 15px;
  text-align: center;
  cursor: pointer;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
}

.operator {
  background-color: #f0f0f0;
}

.zero {
  grid-column: span 2;
}
</style>
