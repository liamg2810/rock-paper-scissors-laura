<script lang="ts">
  import { fly } from "svelte/transition";
  let playerChoice: string;

  function makeChoice(choice: string) {
    playerChoice = choice;
  }
</script>

<div class="game">
  <button on:click={() => makeChoice("rock")}>Rock</button>
  <button on:click={() => makeChoice("paper")}>Paper</button>
  <button on:click={() => makeChoice("scissors")}>Scissors</button>

  {#if playerChoice}
    <div
      class="choice"
      transition:fly={{ x: 200, y: -100, duration: 500 }}
      style="top: 50%; left: 50%;"
    >
      {playerChoice}
    </div>
  {/if}
</div>

<style>
  :global(body) {
    margin: 0;
    font-family: sans-serif;
  }

  .choice {
    position: absolute;
  }

  .game {
    width: 100vw;
    height: 100vh;
  }
</style>
