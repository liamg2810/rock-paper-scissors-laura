<script lang="ts">
  import Checkmark from "$lib/assets/checkmark.svelte";
  import paper from "$lib/assets/paper.png";
  import rock from "$lib/assets/rock.png";
  import scissors from "$lib/assets/scissors.png";

  let playerChoice: string;
  let madeChoice = false;

  function makeChoice(choice: string) {
    playerChoice = choice;
  }
</script>

<div class="game">
  <h1>Rock Paper Scissors</h1>

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

    {#if !madeChoice}
      <button
        class="btn-confirm"
        on:click={() => {
          madeChoice = true;
        }}
      >
        <Checkmark />
      </button>
    {/if}
  {/if}
  <a
    href="https://www.vecteezy.com/free-vector/rock-paper-scissors"
    class="attribution">Rock Paper Scissors Vectors by Vecteezy</a
  >
</div>

<style>
  :global(body) {
    margin: 0;
  }

  h1 {
    position: absolute;
    top: 5%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: "DynaPuff", system-ui;
    font-size: 3rem;
  }

  .btn-choice {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0);
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: 3px solid black;
    background-color: rgb(159, 241, 255);
    transition: all 0.3s;
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

  .attribution {
    position: absolute;
    bottom: 0;
    right: 0;
    padding: 10px;
    font-size: 12px;
    color: #333;
    text-decoration: none;
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
    background: linear-gradient(125deg, #00ff00, #007700);
    transform: translate(-50%, 50%) scale(1.1);
  }
</style>
