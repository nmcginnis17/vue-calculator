<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear" class="specials">AC</div>
    <div @click="sign" class="specials">+/-</div>
    <div @click="percentage" class="specials">%</div>
    <div @click="divide" class="functions">÷</div>
    <div @click="append('7')" class="numbers">7</div>
    <div @click="append('8')" class="numbers">8</div>
    <div @click="append('9')" class="numbers">9</div>
    <div @click="multiply" class="functions">x</div>
    <div @click="append('4')" class="numbers">4</div>
    <div @click="append('5')" class="numbers">5</div>
    <div @click="append('6')" class="numbers">6</div>
    <div @click="subtraction" class="functions">-</div>
    <div @click="append('1')" class="numbers">1</div>
    <div @click="append('2')" class="numbers">2</div>
    <div @click="append('3')" class="numbers">3</div>
    <div @click="addition" class="functions">+</div>
    <div @click="append('0')" class="zero">0</div>
    <div @click="dot" class="numbers">.</div>
    <div @click="equals" class="functions">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      prev: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percentage() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrev() {
      this.prev = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrev();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrev();
    },
    subtraction() {
      this.operator = (a, b) => a - b;
      this.setPrev();
    },
    addition() {
      this.operator = (a, b) => a + b;
      this.setPrev();
    },
    equals() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.prev)
      )}`;
      this.prev = null;
    },
    lastclicked() {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  color: #fff;
  display: grid;
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  text-align: right;
  padding-right: 5%;
}

.numbers {
  /* background-color: gray; */
  border: 2px solid #fff;
  border-radius: 10px;
  margin: 1%;
}

.zero {
  grid-column: 1 / 3;
  text-align: left;
  padding-left: 22%;
  border: 2px solid #fff;
  border-radius: 10px;
  margin: .5%;
  font-size: 40px;
}

.functions {
  border: 2px solid orange;
  border-radius: 10px;
  margin: 1%;
}

.specials {
  border: 2px solid gray;
  border-radius: 10px;
  margin: 1%;
}
</style>
