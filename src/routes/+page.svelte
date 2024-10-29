<script lang="ts">
  import bgMusic from "$lib/assets/bg-music.mp3";
  import click from "$lib/assets/click.mp3";
  import plop from "$lib/assets/plop.mp3";
  import EndGame from "$lib/components/EndGame.svelte";
  import Menu from "$lib/components/Menu.svelte";
  import UserChoice from "$lib/components/UserChoice.svelte";

  import { onMount, tick } from "svelte";

  let clickAudio: HTMLAudioElement;
  let plopAudio: HTMLAudioElement;
  let bgMusicAudio: HTMLAudioElement;

  let gameState: string = "menu";

  let playerChoice: string;
  let computerChoice: string;
  let result: string;

  function EndGameHandler(ev: CustomEvent<any>) {
    gameState = "end";
    playerChoice = ev.detail.choice;
    computerChoice = ["rock", "paper", "scissors"][
      Math.floor(Math.random() * 3)
    ];

    if (
      (playerChoice === "rock" && computerChoice === "scissors") ||
      (playerChoice === "paper" && computerChoice === "rock") ||
      (playerChoice === "scissors" && computerChoice === "paper")
    ) {
      result = "You Win!";
    } else if (playerChoice === computerChoice) {
      result = "It's a Draw!";
    } else {
      result = "You Lose!";
    }
  }

  function RestartGame() {
    gameState = "menu";
    playerChoice = "";
    computerChoice = "";
    result = "";
  }

  function PlaySoundOnHover(event: Event) {
    if (event.target instanceof HTMLButtonElement) {
      plopAudio.play();
    }
  }

  async function UpdateButtonListeners(_: string) {
    await tick();

    document.querySelectorAll("button").forEach((button) => {
      button.addEventListener("mouseover", PlaySoundOnHover);
    });
  }

  $: UpdateButtonListeners(gameState);

  onMount(() => {
    clickAudio = new Audio(click);
    plopAudio = new Audio(plop);
    bgMusicAudio = new Audio(bgMusic);

    bgMusicAudio.loop = true;
    bgMusicAudio.play();

    window.addEventListener("click", PlayClickSound);

    UpdateButtonListeners(gameState);

    return () => {
      window.removeEventListener("click", PlayClickSound);
      document.querySelectorAll("button").forEach((button) => {
        button.removeEventListener("mouseover", PlaySoundOnHover);
      });
    };
  });

  function PlayClickSound() {
    clickAudio.play();
  }
</script>

<div class="game">
  <h1 class="title">Rock Paper Scissors</h1>

  {#if gameState === "menu"}
    <Menu
      on:start-game={() => {
        gameState = "game";
      }}
    />
  {:else if gameState === "game"}
    <UserChoice
      on:choice-made={EndGameHandler}
      on:update-button-audio={() => {
        UpdateButtonListeners("");
      }}
    />
  {:else if gameState === "end"}
    <EndGame
      userChoice={playerChoice}
      {computerChoice}
      {result}
      on:playAgain={RestartGame}
    />
  {/if}
</div>

<a
  href="https://www.vecteezy.com/free-vector/rock-paper-scissors"
  class="attribution">Rock Paper Scissors Vectors by Vecteezy</a
>

<style>
  :global(body) {
    margin: 0;
  }

  .title {
    position: absolute;
    top: 5%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-family: "DynaPuff", system-ui;
    font-size: 3rem;
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
</style>
