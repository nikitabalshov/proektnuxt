<template>
    <div class="tic-tac-toe">
      <h1>Крестики-нолики</h1>
      <div class="board">
        <div
          v-for="(cell, index) in board"
          :key="index"
          class="cell"
          :class="{ 'cell-x': cell === 'X', 'cell-o': cell === 'O' }"
          @click="makeMove(index)"
        >
          {{ cell }}
        </div>
      </div>
      <div class="status">
        <p v-if="winner">{{ winner }} победил!</p>
        <p v-else-if="isDraw">Ничья!</p>
        <p v-else>Ход: {{ currentPlayer }}</p>
      </div>
      <button @click="resetGame" class="reset-button">Начать заново</button>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const board = ref(Array(9).fill(null)); 
  const currentPlayer = ref('X'); 
  const winner = ref(null);
  const isDraw = ref(false);
  
  function makeMove(index) {
    if (!board.value[index] && !winner.value) {
      board.value[index] = currentPlayer.value;
      if (checkWinner()) {
        winner.value = currentPlayer.value;
      } else if (board.value.every((cell) => cell)) {
        isDraw.value = true;
      } else {
        currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X';
      }
    }
  }
  
  function checkWinner() {
    const winningCombinations = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6],
    ];
  
    return winningCombinations.some(
      ([a, b, c]) =>
        board.value[a] &&
        board.value[a] === board.value[b] &&
        board.value[a] === board.value[c]
    );
  }
  
  function resetGame() {
    board.value = Array(9).fill(null);
    currentPlayer.value = 'X';
    winner.value = null;
    isDraw.value = false;
  }
  </script>
  
  <style scoped>
  .tic-tac-toe {
    text-align: center;
    font-family: Arial, sans-serif;
  }
  
  .board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    gap: 5px;
    justify-content: center;
    margin: 20px auto;
  }
  
  .cell {
    width: 100px;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    font-weight: bold;
    border: 2px solid #ccc;
    cursor: pointer;
    background-color: #f9f9f9;
    transition: background-color 0.3s;
  }
  
  .cell:hover {
    background-color: #eaeaea;
  }
  
  .cell-x {
    color: #ff5722;
  }
  
  .cell-o {
    color: #2196f3;
  }
  
  .status {
    margin: 20px 0;
    font-size: 1.2rem;
  }
  
  .reset-button {
    padding: 10px 20px;
    font-size: 1rem;
    border: none;
    border-radius: 5px;
    background-color: #4caf50;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .reset-button:hover {
    background-color: #45a049;
  }
  </style>