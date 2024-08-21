<template>
  <div class="container">
    <CalculatorDisplay :value="result" />
    <CalculatorButton
      v-for="num in numbers"
      :key="num"
      :label="num"
      type="num"
      :handleClick="() => handleInput(num)"
    />
    <CalculatorButton
      v-for="oper in operations"
      :key="oper"
      :label="oper"
      type="num"
      :handleClick="() => handleInput(oper)"
    />
    <CalculatorButton label="=" type="num" :handleClick="calculateResult" />
    <CalculatorButton label="←" type="num" :handleClick="handleDelete" />
    <CalculatorButton label="C" type="delete" :handleClick="clearDisplay" />
  </div>
</template>

<script>
import CalculatorDisplay from './components/CalculatorDisplay.vue';
import CalculatorButton from './components/CalculatorButton.vue';

export default {
  components: {
    CalculatorDisplay,
    CalculatorButton,
  },
  data() {
    return {
      result: '',
      hasDecimal: false,
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0, '.'],
      operations: ['+', '-', '*', '/'],
    };
  },
  methods: {
    handleInput(char) {
      if (char === '.') {
        if (this.hasDecimal || this.result === '' || this.operations.includes(this.result.slice(-1))) {
          return;
        }
        this.hasDecimal = true;
      } else if (this.operations.includes(char)) {
          if (this.result === '' || this.operations.includes(this.result.slice(-1))) {
            return;
          }
        this.hasDecimal = false;
      }
      this.result += char;
    },
    clearDisplay() {
      this.result = '';
      this.hasDecimal = false;
    },
    calculateResult() {
      try {
        this.result = this.result === '' ? '' : String(eval(this.result));
      } catch (error) {
        this.result = 'Error';
      }
    },
    handleDelete() {
      if (this.result.slice(-1) === '.') {
        this.hasDecimal = false;
      }
      this.result = this.result.slice(0, -1);
    }
  },
};
</script>

<style scoped></style>