<script>
  import paper from "$lib/assets/paper.png";
  import rock from "$lib/assets/rock.png";
  import scissors from "$lib/assets/scissors.png";
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
  <div class="choices-holder">
    <div class="choices">
      <div class="choice">
        Your Choice
        <img
          src={rock}
          alt="rock"
          class="choice-rock"
          class:selected-choice={userChoice == "rock"}
        />
        <img
          src={paper}
          alt="paper"
          class="choice-paper"
          class:selected-choice={userChoice == "paper"}
        />
        <img
          src={scissors}
          alt="scissors"
          class="choice-scissors"
          class:selected-choice={userChoice == "scissors"}
        />
      </div>
      <div class="choices">
        <div class="choice">
          Computer Choice
          <img
            src={rock}
            alt="rock"
            class="choice-rock"
            class:selected-choice={computerChoice == "rock"}
          />
          <img
            src={paper}
            alt="paper"
            class="choice-paper"
            class:selected-choice={computerChoice == "paper"}
          />
          <img
            src={scissors}
            alt="scissors"
            class="choice-scissors"
            class:selected-choice={computerChoice == "scissors"}
          />
        </div>
      </div>
    </div>
  </div>

  <div class="result">
    <p>{result}</p>
    <button class="btn-play-again" on:click={playAgain}>Play Again</button>
  </div>
</div>

<style>
  .end-game {
    text-align: center;
    margin-top: 20px;
  }

  .choices-holder {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    margin: 10px 0;
  }

  .choices {
    display: flex;
    gap: 20rem;
  }

  .result {
    font-size: 1.5em;
    margin: 10px 0;
  }

  .choice {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    font-size: 2rem;
    font-family: "DynaPuff", system-ui;
    gap: 30px;
  }

  .choice img {
    user-select: none;
    -webkit-user-select: none;
    pointer-events: none;
    width: 100px;
    height: 100px;
    margin: 0 10px;
    display: none;
    background-color: rgba(255, 255, 255, 0.4);
    border-radius: 50%;
    padding: 10px;
  }

  .choice .selected-choice {
    display: block;
  }

  .result {
    font-size: 2rem;
    font-family: "DynaPuff", system-ui;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }

  .btn-play-again {
    padding: 10px 20px;
    font-size: 1em;
    cursor: pointer;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
    transition: all 0.3s ease;
    font-family: "DynaPuff", system-ui;
  }

  .btn-play-again:hover {
    background-color: #0056b3;
    scale: 1.1;
  }

  .btn-play-again:active {
    background-color: #004085;
  }
</style>
