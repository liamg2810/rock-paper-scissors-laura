<script lang="ts">
  import paper from "$lib/assets/paper.png";
  import rock from "$lib/assets/rock.png";
  import scissors from "$lib/assets/scissors.png";
  import { fly } from "svelte/transition";
  let playerChoice: string;

  function makeChoice(choice: string) {
    playerChoice = choice;
  }
</script>

<div class="game">
  <button
    on:click={() => makeChoice("rock")}
    class="btn-choice btn-rock selecting"
  >
    <img src={rock} alt="rock" /></button
  >
  <button
    on:click={() => makeChoice("paper")}
    class="btn-choice btn-paper selecting"
    ><img src={paper} alt="paper" /></button
  >
  <button
    on:click={() => makeChoice("scissors")}
    class="btn-choice btn-scissors selecting"
    ><img src={scissors} alt="scissors" /></button
  >

  {#if playerChoice}
    <div class="choice" style="top: 50%; left: 50%;">
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
  {/if}
</div>

<style>
  :global(body) {
    margin: 0;
    font-family: sans-serif;
  }

  .btn-choice {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: 3px solid black;
    background-color: rgb(159, 241, 255);
  }

  img {
    pointer-events: none;
    user-select: none;
    -webkit-user-select: none;
  }

  .btn-rock.selecting {
    top: 30%;
    left: 40%;
    transform: translate(-50%, -50%) rotate(-45deg);
  }

  .btn-paper.selecting {
    top: 30%;
    left: 60%;
    transform: translate(-50%, -50%) rotate(45deg);
  }

  .btn-scissors.selecting {
    top: 70%;
    transform: translate(-50%, -50%);
  }

  .btn-choice img {
    width: 100%;
    height: 100%;
  }

  .choice {
    position: absolute;
    left: 50%;
    top: 50%;
    margin: -5px;
    transform: translate(-50%, -50%);
    width: 100px;
    height: 100px;
  }

  .choice img {
    display: none;
    width: 100%;
    height: 100%;
    padding: 5px;
    background-color: rgba(255, 255, 255, 0.4);
    border-radius: 50%;
  }

  .choice .selected-choice {
    display: block;
  }

  .game {
    position: relative;
    width: 100vw;
    height: 100vh;
    background-color: #fefefe;
    background-image: repeating-linear-gradient(
        45deg,
        #ffb10a 25%,
        transparent 25%,
        transparent 75%,
        #ffb10a 75%,
        #ffb10a
      ),
      repeating-linear-gradient(
        45deg,
        #ffb10a 25%,
        #ffd739 25%,
        #ffd739 75%,
        #ffb10a 75%,
        #ffb10a
      );
    background-position:
      0 0,
      96px 96px;
    background-size: 192px 192px;
    overflow: hidden;
    animation: moveBackground 10s linear infinite;
  }

  @keyframes moveBackground {
    0% {
      background-position:
        0 0,
        96px 96px;
    }
    100% {
      background-position:
        96px 96px,
        192px 192px;
    }
  }
</style>
