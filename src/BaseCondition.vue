<template>
  <div class="calculator">
    <h1>Simple Calculator</h1>
    <div class="calculator-inputs">
      <div class="input-row">
        <input class="input1" type="number" v-model="operand1" placeholder="Operand 1">
      </div>
      <div class="input-row">
        <select v-model="operator">
          <option value="+">+</option>
          <option value="-">-</option>
          <option value="*">*</option>
          <option value="/">/</option>
        </select>
      </div>
      <div class="input-row">
        <input class="input2" type="number" v-model="operand2" placeholder="Operand 2">
      </div>
    </div>
    <p class="calculator-result">Result: {{ calculateResult() }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      operand1: 0,
      operand2: 0,
      operator: '+',
    };
  },
  methods: {
    calculateResult() {
      const num1 = parseFloat(this.operand1);
      const num2 = parseFloat(this.operand2);

      switch (this.operator) {
        case '+':
          return num1 + num2;
        case '-':
          return num1 - num2;
        case '*':
          return num1 * num2;
        case '/':
          if (num2 !== 0) {
            return num1 / num2;
          } else {
            return 'Division by zero';
          }
        default:
          return 'Invalid Operator';
      }
    },
  },
};
</script>

<style scoped>
.calculator {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  background: linear-gradient(to bottom, #2a93da, #880eb8);
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 50);
  text-align: center;
  margin-top: 90px;
}

.calculator h1 {
  font-size: 35px;
  margin-bottom: 20px;
}

.calculator-inputs {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-bottom: 20px;
}

.input-row {
  margin-bottom: 10px;
}

.calculator-inputs input,
.calculator-inputs select {
  width: 95%;
  padding: 10px;
  font-size: 16px;
}

.calculator-result {
  margin-top: 0;
}

.calculator-result p {
  font-size: 18px;
  font-weight: bold;
  color: #fff;
}
</style>
