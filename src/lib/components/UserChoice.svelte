<script lang="ts">
  import Checkmark from "$lib/assets/checkmark.svelte";
  import paper from "$lib/assets/paper.png";
  import rock from "$lib/assets/rock.png";
  import scissors from "$lib/assets/scissors.png";
  import { createEventDispatcher } from "svelte";

  let dispatch = createEventDispatcher();

  let playerChoice: string;
  let madeChoice = false;

  function makeChoice(choice: string) {
    playerChoice = choice;
  }

  function ConfirmChoice() {
    madeChoice = true;
    setTimeout(() => {
      dispatch("choice-made", { choice: playerChoice });
    }, 1000);
  }
</script>

<!-- Choices on the sides -->
<button
  on:click={() => makeChoice("rock")}
  class="btn-choice btn-rock"
  class:selecting={!madeChoice}
>
  <img src={rock} alt="rock" /></button
>
<button
  on:click={() => makeChoice("paper")}
  class="btn-choice btn-paper"
  class:selecting={!madeChoice}><img src={paper} alt="paper" /></button
>
<button
  on:click={() => makeChoice("scissors")}
  class="btn-choice btn-scissors"
  class:selecting={!madeChoice}><img src={scissors} alt="scissors" /></button
>

<!-- Choice displayed in the middle -->
{#if playerChoice}
  <div class="choice" class:choice-confirmed={madeChoice}>
    <img
      src={rock}
      alt="rock"
      class="choice-rock"
      class:selected-choice={playerChoice == "rock"}
    />
    <img
      src={paper}
      alt="paper"
      class="choice-paper"
      class:selected-choice={playerChoice == "paper"}
    />
    <img
      src={scissors}
      alt="scissors"
      class="choice-scissors"
      class:selected-choice={playerChoice == "scissors"}
    />
  </div>

  {#if !madeChoice}
    <button class="btn-confirm" on:click={ConfirmChoice}>
      <Checkmark />
    </button>
  {/if}
{/if}

<style>
  .btn-choice {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0.00001);
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: 3px solid black;
    background-color: rgb(159, 241, 255);
    transition: all 0.6s;
  }

  img {
    pointer-events: none;
    user-select: none;
    -webkit-user-select: none;
  }

  .btn-rock.selecting {
    top: 30%;
    left: 40%;
    transform: translate(-50%, -50%) rotate(-45deg) scale(1);
  }

  .btn-paper.selecting {
    top: 30%;
    left: 60%;
    transform: translate(-50%, -50%) rotate(45deg) scale(1);
  }

  .btn-scissors.selecting {
    top: 70%;
    transform: translate(-50%, -50%) scale(1);
  }

  .btn-choice img {
    width: 100%;
    height: 100%;
  }

  .btn-choice:hover {
    transform: translate(-50%, -50%) scale(1.1);
  }

  .choice {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    width: 100px;
    height: 100px;
    border-radius: 50%;
    margin: -5px;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    background-color: rgba(255, 255, 255, 0.4);
  }

  .choice-confirmed {
    transition: all 1s;
    transform-origin: center;
    transform: translate(-50%, -50%) scale(0) rotate(1800deg);
  }

  .choice img {
    display: none;
    padding: 5px;
    width: 90px;
    height: 90px;
  }

  .choice .selected-choice {
    display: block;
  }

  .btn-confirm {
    position: absolute;
    bottom: 10%;
    left: 50%;
    transform: translate(-50%, 50%);
    width: 70px;
    height: 70px;
    border-radius: 50%;
    padding: 10px;
    background: linear-gradient(125deg, #00ff00, #007700);
    border: 3px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.2s;
  }

  .btn-confirm:hover {
    transform: translate(-50%, 50%) scale(1.1);
  }
</style>
