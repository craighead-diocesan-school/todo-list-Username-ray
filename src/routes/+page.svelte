<script>
  import Header from "$lib/Header.svelte"

  let tasks = []

  function addTask() {
    const oldTasks = tasks
    const newTask = ""

    tasks = [...oldTasks, newTask]
  }

  function removeTask(index) {
    const firstPart = tasks.slice(0, index)
    const secondPart = tasks.slice(index + 1)

    tasks = [...firstPart, ...secondPart]
  }

  function saveTasks() {
    const tasksAsJSON = JSON.stringify(tasks)
    localStorage.todos = tasksAsJSON
  }

  function loadTasks() {
    const tasksAsJSON = localStorage.todos
    const tasksAsArray = JSON.parse(tasksAsJSON)

    tasks = tasksAsArray
  }
</script>

<Header />

<main>
  <h2>SvelteKit</h2>

  <p>Welcome to coding with SvelteKit, a modern JavaScript framework that makes it easy to code great apps.</p>

  <button on:click={addTask}>📝 Add</button>
  <button on:click={saveTasks}>💾 Save</button>
  <button on:click={loadTasks}>📡 Load</button>

  {#each tasks as task, index}
    <div class="task">
      <input bind:value={tasks[index]} />
      <button
        on:click={() => {
          removeTask(index)
        }}>🗑</button
      >
    </div>
  {/each}
</main>

<footer>
  <p>&copy; Craighead Diocesan School 2024</p>
</footer>

<style>
  .task {
    display: block;
  }
</style>
