<template>
  <div class="container mx-auto h-[100vh]">
    <div class="w-72 pb-5 bg-slate-600">
      <h1 id="currentValue">{{ currentValue }}</h1>
      <div class="pl-6 pt-3">
        <button
          v-for="(number, key) in numbers"
          @click="append(number)"
          :key="key"
        >
          {{ number }}
        </button>
        <button
          v-for="(method, key) in methods"
          @click="
            if (method === 'C') {
              clearNumber();
            } else if (method !== '=') {
              append(method);
            } else {
              calculate();
            }
          "
          :disabled="currentValue.length === 0"
          :key="key"
        >
          {{ method }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // create 9 buttons of numbers
  // create 2 method buttons + -
  // Show the current number
  data() {
    return {
      currentValue: "",
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      methods: ["+", "-", "/", "*", "=", "%", "C"],
    };
  },
  methods: {
    append(number) {
      if (
        !this.currentValue.match(/^[^a-zA-Z0-9]+$/) ||
        this.currentValue.length !== 0
      ) {
        this.currentValue = this.currentValue + number;
      }
    },
    calculate() {
      let convertedNumber = this.convert(this.currentValue);
      this.currentValue = convertedNumber;
    },
    clearNumber() {
      this.currentValue = "";
    },
    convert(str) {
      let output;

      if (str.includes("+")) {
        output = Number(str.split("+")[0]) + Number(str.split("+")[1]);
      } else if (str.includes("-")) {
        output = Number(str.split("-")[0]) - Number(str.split("-")[1]);
      } else if (str.includes("/")) {
        output = Number(str.split("/")[0]) / Number(str.split("/")[1]);
      } else if (str.includes("*")) {
        output = Number(str.split("*")[0]) * Number(str.split("*")[1]);
      } else {
        output = Number(str.split("%")[0]) % Number(str.split("%")[1]);
      }
      return output.toString();
    },
  },
};
</script>

<style scoped>
button {
  width: 52px;
  height: 52px;
  margin: 5px;
  padding: 0;
  background-color: dodgerblue;
}
h1#currentValue {
  display: flex;
  align-items: center;
  justify-content: left;
  background: lightgray;
  padding: 10px;
}
</style>
