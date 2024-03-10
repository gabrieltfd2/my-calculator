<template>
  <div class="calculator">
    <div class="inputs">
      <input type="number" v-model="number1" @input="calculate">
      <select v-model="operator" @change="calculate">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="x">×</option>
        <option value="÷">÷</option>
      </select>
      <input type="number" v-model="number2" @input="calculate">
    </div>
    <div class="display">{{ result }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number1: '',
      number2: '',
      operator: '+',
      result: ''
    };
  },
  methods: {
    calculate() {
      const num1 = parseFloat(this.number1);
      const num2 = parseFloat(this.number2);

      if (!isNaN(num1) && !isNaN(num2)) {
        switch (this.operator) {
          case '+':
            this.result = num1 + num2;
            break;
          case '-':
            this.result = num1 - num2;
            break;
          case 'x':
            this.result = num1 * num2;
            break;
          case '÷':
            if (num2 !== 0) {
              this.result = num1 / num2;
            } else {
              this.result = 'Error: Division by zero';
            }
            break;
          default:
            this.result = '';
            break;
        }
      } else {
        this.result = '';
      }
    }
  }
};
</script>

<style scoped>
.calculator {
  max-width: 500px;
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

.inputs {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.inputs input[type="number"],
.inputs select {
  font-size: 16px;
  padding: 8px;
  margin-right: 10px;
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
