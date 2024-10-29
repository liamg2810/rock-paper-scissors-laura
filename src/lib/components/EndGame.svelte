<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let userChoice;
  export let computerChoice;
  export let result;

  function playAgain() {
    // Dispatch a custom event to notify the parent component to reset the game
    dispatch("playAgain");
  }
</script>

<div class="end-game">
  <div class="choices">
    <p>User Choice: {userChoice}</p>
    <p>Computer Choice: {computerChoice}</p>
  </div>
  <div class="result">
    <p>{result}</p>
  </div>
  <button on:click={playAgain}>Play Again</button>
</div>

<style>
  .end-game {
    text-align: center;
    margin-top: 20px;
  }
  .choices {
    margin: 10px 0;
  }
  .result {
    font-size: 1.5em;
    margin: 10px 0;
  }
  button {
    padding: 10px 20px;
    font-size: 1em;
    cursor: pointer;
  }
</style>
