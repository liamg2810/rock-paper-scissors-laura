<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function startGame() {
    dispatch("start-game");
  }
</script>

<div class="menu-container">
  <button class="btn-start" on:click={startGame}>Start Game</button>
</div>

<style>
  .menu-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .btn-start {
    padding: 10px 20px;
    font-size: 2rem;
    cursor: pointer;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    transition: all 0.3s ease;
    font-family: "DynaPuff", system-ui;
  }

  .btn-start:hover {
    background-color: #0056b3;
    scale: 1.1;
  }

  .btn-start:active {
    background-color: #004085;
  }
</style>
