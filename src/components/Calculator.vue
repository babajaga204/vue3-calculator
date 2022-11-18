<template>
  <div class="calculator">
    <div class="calculator-display">{{ displayValue }}</div>
    <div class="calculator-keys">
      <button
        @click="concatOp('+')"
        class="operator plus">
        +
      </button>
      <button
        @click="concatOp('-')"
        class="operator minus">
        -
      </button>
      <button
        @click="concatOp('*')"
        class="operator multiply">
        &times;
      </button>
      <button
        @click="concatOp('/')"
        class="operator divide">
        ÷
      </button>
      <button
        @click="concatNum('0')"
        class="number zero">
        0
      </button>
      <button
        @click="concatNum('1')"
        class="number one">
        1
      </button>
      <button
        @click="concatNum('2')"
        class="number two">
        2
      </button>
      <button
        @click="concatNum('3')"
        class="number three">
        3
      </button>
      <button
        @click="concatNum('4')"
        class="number four">
        4
      </button>
      <button
        @click="concatNum('5')"
        class="number five">
        5
      </button>
      <button
        @click="concatNum('6')"
        class="number six">
        6
      </button>
      <button
        @click="concatNum('7')"
        class="number seven">
        7
      </button>
      <button
        @click="concatNum('8')"
        class="number eight">
        8
      </button>
      <button
        @click="concatNum('9')"
        class="number nine">
        9
      </button>
      <button
        @click="concatNum('.')"
        class="decimal">
        .
      </button>
      <button
        @click="clear()"
        class="clear">
        C
      </button>
      <button
        @click="calculate()"
        class="equal">
        =
      </button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    let displayValue = ref("0");
    let firstNumber = "";
    let operator = null;

    function concatNum(num) {
      if (operator === null) {
        displayValue.value === "0"
          ? (displayValue.value = num)
          : (displayValue.value += num);
      } else if (["+", "-", "*", "/"].includes(operator)) {
        displayValue.value === firstNumber
          ? (displayValue.value = num)
          : (displayValue.value += num);
      }
    }

    function concatOp(op) {
      firstNumber = displayValue.value;
      operator = op;
    }

    function clear() {
      displayValue.value = "0";
      firstNumber = "";
      operator = null;
    }

    function calculate() {
      displayValue.value = eval(firstNumber + operator + displayValue.value);
      firstNumber = displayValue.value;
    }

    return { displayValue, concatNum, concatOp, clear, calculate };
  },
};
</script>

<style scoped>
button {
  padding: 1rem;
  border: none;
}

.calculator {
  /* border: red solid 2px; */
  display: flex;
  flex-direction: column;
  border-radius: 0.5rem;
  overflow: hidden;
  box-shadow: 0 0 20px -5px;
}

.calculator-display {
  background-color: rgb(39, 44, 55);
  width: 16.25rem;
  height: auto;
  padding: 0.75rem 1rem;
  text-align: right;
  font-size: x-large;
  color: rgb(226, 226, 226);
}

.calculator-keys {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-areas:
    ".  .  .  ."
    "seven eight nine equal"
    "four five six equal"
    "one two three equal"
    "zero decimal clear equal";
}

.one {
  grid-area: one;
}
.two {
  grid-area: two;
}
.three {
  grid-area: three;
}
.four {
  grid-area: four;
}
.five {
  grid-area: five;
}
.six {
  grid-area: six;
}
.seven {
  grid-area: seven;
}
.eight {
  grid-area: eight;
}
.nine {
  grid-area: nine;
}
.zero {
  grid-area: zero;
}

.decimal {
  grid-area: decimal;
}
.clear {
  grid-area: clear;
}
.equal {
  grid-area: equal;
  background-color: rgb(255, 163, 3);
  border: 1px darkgrey solid;
}

.equal:hover,
.equal:focus {
  background-color: rgb(196, 128, 0);
}

.number:hover,
.number:focus {
  background-color: rgb(174, 174, 174);
}

.decimal:hover,
.decimal:focus {
  background-color: rgb(174, 174, 174);
}

.clear:hover,
.clear:focus {
  background-color: rgb(174, 174, 174);
}

.operator:hover,
.operator:focus {
  background-color: rgb(174, 174, 174);
}
.operator {
  border: 1px darkgrey solid;
}

.number,
.decimal,
.clear {
  background-color: lightgrey;
  border: 1px darkgrey solid;
}
</style>
