<script>
  import Todo from "./todo.svelte";
</script>

<main>
  <div class="container">
    <div id="top-right">Need to do Quickly</div>
    <div id="top-left">Should be done quickly</div>

    <div id="bottom-left">Needs to be done</div>
    <div id="bottom-right">Not really needed</div>
  </div>
  <Todo />
</main>

<style>
  #top-right {
    background-color: #ff3e00;
  }

  #top-left {
    background-color: aqua;
  }

  #bottom-left {
    background-color: yellow;
  }
  .container {
    position: relative;
    display: grid;
    grid-template-columns: 1fr 1fr;
    height: 100vh;
    width: 100vw;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
