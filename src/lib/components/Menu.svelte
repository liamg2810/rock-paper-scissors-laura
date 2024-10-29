<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function startGame() {
    dispatch("start-game");
  }
</script>

<div class="menu-container">
  <button class="start-button" on:click={startGame}>Start Game</button>
</div>

<style>
  .menu-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .start-button {
    padding: 15px 30px;
    font-size: 18px;
    font-weight: bold;
    color: #fff;
    background-color: #007bff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .start-button:hover {
    background-color: #0056b3;
    scale: 1.1;
  }

  .start-button:active {
    background-color: #004085;
  }
</style>
