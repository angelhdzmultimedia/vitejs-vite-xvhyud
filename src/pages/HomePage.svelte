<script>
import Button from '../components/Button.svelte'
import Fa from 'svelte-fa'
  import { faTrash } from '@fortawesome/free-solid-svg-icons'
  
  let tasks = [
    {
      name: 'Task #1',
      id: Date.now(),
      isDone: false
    }
  ]

  let activeFilter = 'all'
  let filters = ['All', 'Pending', 'Done']

  let filteredTasks = []
  $: {
    activeFilter === 'pending' 
    ? filteredTasks = tasks.filter(item => !item.isDone)
    : activeFilter === 'done'
    ? filteredTasks = tasks.filter(item => item.isDone)
    : filteredTasks = tasks
  }

  function deleteTask(task) {
    tasks = tasks.filter(item => item !== task)
  }
  let newTask = ''

  function addTask() {
    tasks = [...tasks, {
      name: newTask,
      id: Date.now(),
      isDone: false
    }]
    newTask = ''
  }
</script>

<main>

<div class="flex flex-col gap-10 items-center">
<span class=" font-bold">Svelte TypeScript To Do List</span>
<div class="flex flex-row gap-2">
{#each filters as filter}
<Button label={filter}></Button>
{/each}
</div>
<div class="tasks flex flex-col w-full">
{#each filteredTasks as task}
  <li class="task flex flex-row justify-between items-center mx-10">
  <div>
  <input type="checkbox">
  <span>{task.name}</span>
  </div>
  <Button on:click={() => deleteTask(task)} icon='faTrash'>
  
  </Button>
  </li>
{/each}
</div>
 <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
        Username
      </label>
      <input bind:value={newTask} class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Task Name">
<Button on:click={addTask} label="Add Task"></Button>
</div>
</main>

<style>
  
  .tasks {

  }

  .task {
    list-style: none;
  }
</style>