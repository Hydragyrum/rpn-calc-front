<template>
  <div>
      <div class="content">
      <div class="calc-body">
        <div id="display" class="display">{{ expression }}</div>
        <button id="btn-equals" class="btn-equals" @click="submit">=</button>
        <button id="btn-plus" class="btn-plus" @click="clicked('+')">+</button>
        <button id="btn-minus" class="btn-minus"@click="clicked('-')">-</button>
        <button id="btn-times" class="btn-times" @click="clicked('*')">x</button>
        <button id="btn-divide" class="btn-divide" @click="clicked('/')">&#247</button>
        <button id="btn-clear" class="btn-clear" @click="clear()">C</button>
        <button id="btn-del" class="btn-del" @click="del()">DEL</button>
        <button id="btn-zero" class="btn-zero" @click="clicked(0)">0</button>
        <button id="btn-one" class="btn-one" @click="clicked(1)">1</button>
        <button id="btn-two" class="btn-two" @click="clicked(2)">2</button>
        <button id="btn-three" class="btn-three" @click="clicked(3)">3</button>
        <button id="btn-four" class="btn-four" @click="clicked(4)">4</button>
        <button id="btn-five" class="btn-five" @click="clicked(5)">5</button>
        <button id="btn-six" class="btn-six" @click="clicked(6)">6</button>
        <button id="btn-seven" class="btn-seven" @click="clicked(7)">7</button>
        <button id="btn-eight" class="btn-eight" @click="clicked(8)">8</button>
        <button id="btn-nine" class="btn-nine" @click="clicked(9)">9</button>
        <button id="btn-dot" class="btn-dot" @click="clicked('.')">.</button>
        <button id="btn-enter" class="btn-enter" @click="clicked(' ')">Enter</button>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Axios, { AxiosResponse } from 'axios';

@Component
export default class Calculator extends Vue {
  public expression: string = '';

  /**
   * submit
   */
  public submit() {
    Axios.get(
      'http://localhost:8008?calc=' + encodeURIComponent(this.expression),
    ).then((response: AxiosResponse) => {
      this.expression = response.data + ' ';
      this.$forceUpdate();
    });
  }

  public clicked(char: string) {
    this.expression += char;
  }

  public clear() {
      this.expression = '';
      this.$forceUpdate();
  }

  public del() {
      this.expression = this.expression.substring(0, this.expression.length - 1);
  }
}
</script>
<style>
/**** General ****/
:root {
  --bg-color: hsla(215, 85%, 20%, 1);
  --display-color: hsla(215, 100%, 72%, 1);
  --off-white: hsla(215, 85%, 95%, 1);
  --light-green: hsla(130, 90%, 65%, 1);
}

* {
  box-sizing: border-box;
  font-family: "Open Sans";
  color: var(--dark-bg-color);
  -webkit-touch-callout: none;
  -webkit-user-select: none; /* Webkit */
  -moz-user-select: none;    /* Firefox */
  -ms-user-select: none;     /* IE 10  */
  border-radius: 3px;
}

button::-moz-focus-inner {
  border: 0;
}

body {
  margin: 0;
  padding: 0;
  background-color: var(--bg-color);
}

.content{
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  min-width: 100vw;
  font-size: 36px;
}

.calc-body {
  height: 100vh;
  width: 100vw;
  display: grid;
  grid-template: 1.5fr 1fr 1fr 1fr 1fr 1fr / 1fr 1fr 1fr 1fr;
  grid-gap: 5px;
  max-height: 640px;
  max-width: 480px;
  padding: 17px;
  box-shadow: 2px 2px 4px 4px hsla(215, 85%, 5%, 1);
  border: 1px solid var(--off-white);
  background: hsla(218, 85%, 10%, 1);
}

.display {
  grid-row: 1;
  grid-column: 1 / 5;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  flex-wrap: wrap-reverse;
  padding-right: 10px;
  padding-left: 10px;
  color: var(--off-white);
  overflow: hidden;
  background-color: var(--display-color);
  margin-bottom: 10px;
  border: 1px solid var(--off-white);
}

/**** Buttons ****/
button {
  background-color: var(--off-white);
  font-size: 2rem;
  border: none;
  color: var(--bg-color);
  text-decoration: none;
}

button,
button:focus,
button:active{
	outline: none;
	padding: 0;
}

button:active {
  background-color: var(--light-green);
}

.btn-equals {
  grid-row: 6;
  grid-column: 3 / 5;
  background: var(--light-green);
}

.btn-equals:active {
  background: hsla(135, 90%, 60%, 1);
}

.btn-plus {
  grid-row: 5;
  grid-column: 4;
}

.btn-minus {
  grid-row: 4;
  grid-column: 4;
}

.btn-times {
  grid-row: 3;
  grid-column: 4;
}

.btn-divide {
  grid-row: 2;
  grid-column: 4;
}

.btn-clear {
  grid-row: 2;
  grid-column: 1;
  background: hsla(1, 75%, 60%, 1);
  color: var(--off-white);
}

.btn-clear:active {
  background: hsla(1, 75%, 50%, 1);
}

.btn-del {
  grid-row: 2;
  grid-column: 2;
  font-size: 1.5rem;
}

.btn-dot {
  grid-row: 6;
  grid-column: 2;
}

.btn-zero {
  grid-row: 6;
  grid-column: 1;
}

.btn-one {
  grid-row: 5;
  grid-column: 1;
}

.btn-two {
  grid-row: 5;
  grid-column: 2;
}

.btn-three {
  grid-row: 5;
  grid-column: 3;
}

.btn-four {
  grid-row: 4;
  grid-column: 1;
}

.btn-five {
  grid-row: 4;
  grid-column: 2;
}

.btn-six {
  grid-row: 4;
  grid-column: 3;
}

.btn-seven {
  grid-row: 3;
  grid-column: 1;
}

.btn-eight {
  grid-row: 3;
  grid-column: 2;
}

.btn-nine {
  grid-row: 3;
  grid-column: 3;
}

.btn-enter {
  grid-row: 2;
  grid-column: 3;
}


/**** Responsive Design ****/
@media screen and (max-width: 420px) , screen and (max-height: 420px) {
  .display {
    font-size: 7vmin;
  }
}
</style>
