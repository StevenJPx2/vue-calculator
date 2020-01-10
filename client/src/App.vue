<template>
  <div id="app">
    <h1>
      Hello<span v-if="name">, {{ name }}</span
      >!
    </h1>
    <div class="container">
      <label for="myname">Name:</label>
      <input
        type="text"
        v-model="name"
        placeholder="Enter your name..."
        name="myname"
      />
    </div>
    <div class="calculator">
      <div id="calcscreen">
        {{ exp }}
        <div id="total">{{ total }}</div>
      </div>
      <div class="calc-grid">
        <div class="sign-grid">
          <button
            :key="sign"
            v-for="sign in ['+', '-', '*', '/']"
            class="calc-button sign-button"
            @click="setSign(sign)"
          >
            {{ sign }}
          </button>
        </div>

        <div class="button-grid">
          <button
            :key="i"
            v-for="i in (1, 10)"
            class="calc-button number-button"
            @click="insert(i % 10)"
          >
            {{ i % 10 }}
          </button>
          <button @click="insert('.')" class="calc-button number-button">
            .
          </button>
          <button @click="clear()" class="calc-button clear-button">
            AC
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  el: "#app",
  data() {
    return {
      name: "",
      exp: "0",
      currentSign: "",
      total: 0
    };
  },
  methods: {
    insert: function(num) {
      if (this.exp == "0") {
        this.exp = "";
      }
      this.exp += num;
      // eslint-disable-next-line no-undef
      this.total = math.eval(this.exp);
      this.currentSign = "";
    },

    setSign: function(sign) {
      if (this.exp != "0" && /\d/.test(this.exp.slice(-1))) {
        this.exp += sign;
      }
      this.currentSign = sign;
    },

    clear: function() {
      this.exp = "0";
      this.total = 0;
    }
  }
};
</script>

<style>
body {
  background: #20262e;
  padding: 20px;
  font-family: "Avenir Next", Helvetica, sans-serif;
}

#app {
  background: #fff;
  border-radius: 4px;
  padding: 20px;
  transition: all 0.2s;
}

li {
  margin: 8px 0;
}

h1 {
  font-weight: bold;
  margin-bottom: 15px;
  font-size: 50px;
}

h2 {
  font-weight: bold;
  margin-bottom: 15px;
}

del {
  color: rgba(0, 0, 0, 0.3);
}

input {
  border: 3px solid #eee;
  border-radius: 60px;
  width: 300px;
  height: 50px;
  padding-left: 20px;
  font-size: 20px;
  transition: border-color 0.2s ease-out;
}

input:focus,
input:hover {
  outline: #6bc4a6;
  border-color: #6bc4a6;
  transition: border-color 0.4s ease-out;
}

label {
  font-size: 20px;
  padding-right: 20px;
}

.container {
  margin-bottom: 30px;
}

.calc-button {
  border: 1px solid #000;
  border-radius: 7px;
  font-size: 20px;
  height: 50px;
  background-color: #eee;
  box-shadow: inset 0px 2px rgba(255, 255, 255, 0.6),
    0px 2px rgba(90, 90, 90, 0.7);
}

.calc-button:hover {
  background-color: #ccc;
}

.calc-button:active {
  background-color: #aaa;
  box-shadow: inset 0px 2px rgba(0, 0, 0, 0.6), 0px 0px rgba(90, 90, 90, 0.7);
  color: #333;
}

.sign-button {
  color: #39ac9b;
}

.sign-button:active {
  color: #2a7e72;
}

.clear-button {
  background-color: #ff1e00;
  color: #fff;
}

.clear-button:hover {
  background-color: #e01a00;
}

.clear-button:active {
  background-color: #c71700;
  color: #fff;
}

.button-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-area: 1/1/3/4;
  grid-gap: 10px 10px;
}

.sign-grid {
  display: grid;
  grid-template-columns: none none none 1fr;
  grid-gap: 10px 10px;
  padding-left: 10px;
}

.calc-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  padding: 15px;
  border: 2px solid #aaa;
  border-radius: 0px 0px 10px 10px;
}

.calculator {
  width: 300px;
  background-color: #eee;
}

#calcscreen {
  height: 90px;
  padding: 0px 30px;
  padding-top: 10px;
  font-family: "Hack", "Source Code", monospace;
  background-color: #333;
  border: 2px solid #000;
  border-radius: 10px 10px 0px 0px;
  box-shadow: inset 0px 2px rgba(255, 255, 255, 0.4);
  text-align: right;
  color: #ddd;
}

#total {
  font-size: 40px;
  display: table-cell;
  vertical-align: middle;
  color: #fff;
}
</style>
