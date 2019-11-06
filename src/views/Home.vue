<template>
  <div class="home">
    <div class="display">
      {{ display }}
    </div>
    <div class="controls">
      <div class="row">
        <div
          class="col btn"
          @click="handleNumbers(7)"
        >
          7
        </div>
        <div
          class="col btn"
          @click="handleNumbers(8)"
        >
          8
        </div>
        <div
          class="col btn"
          @click="handleNumbers(9)"
        >
          9
        </div>
        <div
          class="col btn"
          @click="handleOperator('/')"
        >
          /
        </div>
        <div
          class="col btn"
          @click="handleBackspace()"
        >
          {{ backspaceButton }}
        </div>
      </div>
      <div class="row">
        <div
          class="col btn"
          @click="handleNumbers(4)"
        >
          4
        </div>
        <div
          class="col btn"
          @click="handleNumbers(5)"
        >
          5
        </div>
        <div
          class="col btn"
          @click="handleNumbers(6)"
        >
          6
        </div>
        <div
          class="col btn"
          @click="handleOperator('*')"
        >
          x
        </div>
        <div class="col"></div>
      </div>
      <div class="row">
        <div
          class="col btn"
          @click="handleNumbers(1)"
        >
          1
        </div>
        <div
          class="col btn"
          @click="handleNumbers(2)"
        >
          2
        </div>
        <div
          class="col btn"
          @click="handleNumbers(3)"
        >
          3
        </div>
        <div
          class="col btn"
          @click="handleOperator('-')"
        >
          -
        </div>
        <div class="col"></div>
      </div>
      <div class="row">
        <div
          class="col btn"
          @click="handleNumbers(0)"
        >
          0
        </div>
        <div class="col btn">.</div>
        <div class="col"></div>
        <div
          class="col btn"
          @click="handleOperator('+')"
        >
          +
        </div>
        <div
          class="col btn"
          @click="handleResult()"
        >
          =
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Home extends Vue {
  private display = '';

  private result = 0;

  private backspaceButton = 'Back';

  private operators = new Set(['+', '-', '%', '*']);

  private handleNumbers(num: number) {
    this.display += num.toString();
  }

  private handleOperator(operator: string) {
    if (!this.display.length) {
      this.display = operator === '-' ? operator : '';
    } else if (this.operators.has(this.display[this.display.length - 1])) {
      const temp = this.display.slice(0, this.display.length - 1) + operator;
      this.display = temp;
    } else {
      this.display += operator;
    }
  }

  private handleBackspace() {
    if (this.display.length && this.backspaceButton === 'Back') {
      this.display = this.display.slice(0, this.display.length - 1);
    } else if (this.backspaceButton === 'C') {
      this.display = '';
      this.backspaceButton = 'Back';
    }
  }

  private handleResult() {
    // eslint-disable-next-line
    this.display = eval(this.display).toString();
    this.backspaceButton = 'C';
  }
}
</script>

<style lang="scss">
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.display {
  display: block;
  height: 64px;
  width: 340px;
  border: 1px solid black;
  border-radius: 15%;
  margin: 4px;
}
.row {
  display: flex;
  height: 64px;
  margin: 4px;
}
.col {
  display: flex;
  width: 64px;
  align-items: center;
  justify-content: center;
  margin: 4px;
}

.btn{
  text-decoration: none;
  background: #5dc3d0;
  color: rgb(82, 142, 150);
  width: 64px;
  height: 64px;
  font-size: 20px;
  line-height: 120px;
  border-radius: 50%;
  text-align: center;
  vertical-align: middle;
  overflow: hidden;
  box-shadow: inset 0px 3px 0 rgba(255,255,255,0.3), 0 3px 3px rgba(0, 0, 0, 0.3);
  font-weight: bold;
  border-bottom: solid 3px #549fa9;
  text-shadow: 1px 1px 1px rgba(255, 255, 255, 0.65);
  transition: .4s;
}

.btn:active{
  -ms-transform: translateY(1px);
  -webkit-transform: translateY(1px);
  transform: translateY(1px);
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.35);
  border-bottom: none;
}
</style>
