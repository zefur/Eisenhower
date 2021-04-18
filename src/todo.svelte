<script>
  export let tasks = [];

  let uid = 1;
  function add(input) {
    const task = {
      id: uid++,
      done: false,
      importance: select.value,
      description: input.value,
    };

    tasks = [task, ...tasks];
    input.value = "";
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

<input
  type="text"
  bind:group={task}
  on:keydown={(e) => e.key === "Enter" && add(e.target)}
/>
<label>
  <select bind:group={task} value="1" />
</label>

<h2>todo</h2>
{#each tasks.filter((t) => !t.done) as todo (todo.id)}
  <label>
    <input type="checkbox" on:change={() => mark(todo, true)} />
    {todo.description}
    <button on:click={() => remove(todo)}>remove</button>
  </label>
{/each}
