<script>
  import UserChoice from "$lib/components/UserChoice.svelte";
</script>

<div class="game">
  <h1>Rock Paper Scissors</h1>

  <UserChoice />
</div>

<a
  href="https://www.vecteezy.com/free-vector/rock-paper-scissors"
  class="attribution">Rock Paper Scissors Vectors by Vecteezy</a
>

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
