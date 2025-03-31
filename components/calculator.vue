<template>
    <div class="calculator">
      <div class="display">{{ current }}</div>
      <div class="buttons">
        <button @click="clear">C</button>
        <button @click="append('/')">/</button>
        <button @click="append('*')">*</button>
        <button @click="append('-')">-</button>
        <button @click="append('7')">7</button>
        <button @click="append('8')">8</button>
        <button @click="append('9')">9</button>
        <button @click="append('+')">+</button>
        <button @click="append('4')">4</button>
        <button @click="append('5')">5</button>
        <button @click="append('6')">6</button>
        <button @click="append('1')">1</button>
        <button @click="append('2')">2</button>
        <button @click="append('3')">3</button>
        <button @click="calculate">=</button>
        <button @click="append('0')" class="zero">0</button>
        <button @click="append('.')">.</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const current = ref('');
  
  function append(value) {
    current.value += value;
  }
  
  function clear() {
    current.value = '';
  }
  
  function calculate() {
    try {
      current.value = eval(current.value).toString();
    } catch {
      current.value = 'Error';
    }
  }
  </script>
  
  <style scoped>
  .calculator {
    width: 300px;
    margin: 0 auto;
    border: 2px solid #ccc;
    border-radius: 10px;
    padding: 20px;
    background: #f9f9f9;
  }
  
  .display {
    height: 50px;
    margin-bottom: 10px;
    background: #eaeaea;
    text-align: right;
    padding: 10px;
    font-size: 1.5rem;
    border-radius: 5px;
    overflow: hidden;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  
  button {
    padding: 15px;
    font-size: 1.2rem;
    border: none;
    border-radius: 5px;
    background: #ddd;
    cursor: pointer;
    transition: background 0.3s;
  }
  
  button:hover {
    background: #ccc;
  }
  
  button.zero {
    grid-column: span 2;
  }
  </style>