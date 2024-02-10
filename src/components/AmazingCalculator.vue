<script setup>
import { ref, computed } from "vue";

const display = ref("0");

const appendToDisplay = (value) => {
  if (display.value === "0" && value !== ".") {
    display.value = value;
  } else {
    display.value += value;
  }
};

const calculate = () => {
  if (display.value.length > 0) {
    try {
      display.value = eval(display.value).toString();
    } catch (error) {
      display.value = "Error";
    }
  }
};

// Computed property for dynamic class binding
const displayClass = computed(() => {
  return display.value.length > 12 ? "small-text" : "";
});

const clearDisplay = () => {
  display.value = "0";
};

const clearOneCharacter = () => {
  if (display.value.length > 0) {
    display.value = display.value.substring(0, display.value.length - 1);
  }
};
</script>

<template>
  <div>
    <div class="calculator">
      <h1>The Best Calculator Ever</h1>

      <input v-model="display" :class="displayClass" />

      <div class="buttons">
        <button @click="appendToDisplay('7')">7</button>
        <button @click="appendToDisplay('8')">8</button>
        <button @click="appendToDisplay('9')">9</button>
        <button @click="appendToDisplay('/')">/</button>

        <button @click="appendToDisplay('4')">4</button>
        <button @click="appendToDisplay('5')">5</button>
        <button @click="appendToDisplay('6')">6</button>
        <button @click="appendToDisplay('*')">*</button>

        <button @click="appendToDisplay('1')">1</button>
        <button @click="appendToDisplay('2')">2</button>
        <button @click="appendToDisplay('3')">3</button>
        <button @click="appendToDisplay('-')">-</button>

        <button @click="appendToDisplay('0')">0</button>
        <button @click="appendToDisplay('.')">.</button>
        <button @click="calculate" class="button-equal">=</button>
        <button @click="appendToDisplay('+')">+</button>
      </div>
      <div class="clear">
        <button @click="clearDisplay" class="clear-button">C</button>
        <button @click="clearOneCharacter" class="delete-one-button">
          DEL
        </button>
      </div>
    </div>
  </div>
</template>

<style>
* {
  font-family: monospace;
}

.calculator {
  max-width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

h1 {
  text-align: center;
  font-size: 1.75rem;
  text-transform: uppercase;
}

input {
  padding: 5px 10px;
  margin-bottom: 20px;
  border-radius: 0px;
  font-size: 18px;
}

.display {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 18px;
  text-align: right;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  width: 100%;
  padding: 10px;
  font-size: 18px;
  background-color: white;
}

.clear {
  display: flex;
  margin-top: 10px;
  gap: 10px;
}

.clear-button {
  flex: 9;
}

.delete-one-button {
  flex: 2;
}

.small-text {
  font-size: 14px;
}
</style>
