<template>
  <div class="calculator">
    <div class="display">{{ current || '0' }}</div> <!-- equal to zero if not defined -->
    <div @click="clear" class="button">C</div>
    <div @click="sign" class="button">+/-</div>
    <div @click="percent" class="button">%</div>
    <div @click="divide" class="button-operator">÷</div>
    <div @click="append('7')" class="button">7</div>
    <div @click="append('8')" class="button">8</div>
    <div @click="append('9')" class="button">9</div>
    <div @click="times" class="button-operator ">*</div>
    <div @click="append('4')" class="button">4</div>
    <div @click="append('5')" class="button">5</div>
    <div @click="append('6')" class="button">6</div>
    <div @click="minus" class="button-operator ">-</div>
    <div @click="append('1')" class="button">1</div>
    <div @click="append('2')" class="button">2</div>
    <div @click="append('3')" class="button">3</div>
    <div @click="add" class="button-operator ">+</div>
    <div @click="append('0')" class="button-zero">0</div>
    <div @click="dot" class="button">.</div>
    <div @click="equal" class="button-operator ">=</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      current: '',
      previous: null,
      operator: null,
      operatorClicked: false,
    }
  },

  methods: {  /* define function by adding methods attribute */
    clear () {
      this.current = '';
    },
    sign () {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1): `-${this.current}`;
    },
    percent () {
      this.current = `${parseFloat(this.current) / 1000}`
    },
    append (number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot () {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      } 
    },
    divide () {
      this.operator = (a, b) => a / b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    times () {
      this.operator = (a, b) => a * b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus () {
      this.operator = (a, b) => a - b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add () {
      this.operator = (a, b) => a + b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal () {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous))
        }`;
        this.previous = null;
    },
  }
}
</script>

<style scoped>
.calculator {
  margin: 0 auto; /* center automatically */
  width: 70%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  border: 1px solid;
  font-size: 2em;
}

.display {
  grid-column: 1 / 5; /*display needs 4 column in the first row start at column 1 and end after column 4*/
  background-color: #B0C4DE;
  border: 1px solid;
}

.button-zero {
  grid-column: 1 / 3;
  background-color: #FFEBCD;
  border: 1px solid;
}

.button {
  background-color: #FFEBCD;
  border: 1px solid;
}

.button-operator {
  background-color: orange;
  text-color: white;
  border: 1px solid;

}
</style>
