<script>
  export let tasks = [];
  let task;
  let importance = 0;
  let urgency = 0;

  let coord = { x: 0, y: 0 };
  let uid = 1;
  function add(input) {
    const task = {
      id: uid++,
      done: false,
      importance: importance,
      urgency: urgency,
      description: input,
    };

    tasks = [task, ...tasks];
    input = "";
  }

  function remove(task) {
    tasks = tasks.filter((t) => t !== task);
  }

  function mark(task, done) {
    task.done = done;
    remove(task);
    tasks = tasks.concat(task);
  }
</script>

<div class="input">
  <h1>What tasks do you need to accomplish?</h1>
  <form on:submit|preventDefault={add(task)}>
    <input
      type="text"
      bind:value={task}
      on:keydown={(e) => e.key === "Enter"}
    />
    <label>
      <input type="range" bind:value={importance} min="0" max="100" />
    </label>
    <label>
      <input type="range" bind:value={urgency} min="0" max="100" />
    </label>
    <button type="submit">Submit</button>
  </form>
</div>

{#each tasks.filter((t) => !t.done) as todo (todo.id)}
  <label class="to" style="left: {todo.importance}%; top:{todo.urgency}%">
    <input type="checkbox" on:change={() => mark(todo, true)} />
    {todo.description}

    <button on:click={() => remove(todo)}>remove</button>
  </label>
{/each}

<style>
  .to {
    position: absolute;
    border: 3px solid green;
    background-color: hotpink;
  }
  .input {
    position: absolute;
    top: 50vh;
    left: 50vw;
    transform: translate(-50%, -50%);
    justify-items: center;
  }
</style>
