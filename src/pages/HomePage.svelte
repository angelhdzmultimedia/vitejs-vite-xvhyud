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

  const FilterStatus = {
    all: 'All',
    pending: 'Pending',
    done: 'Done'
  }

  let activeFilter = FilterStatus.all
  let filters = ['All', 'Pending', 'Done']

  let filteredTasks = []
  $: {
    activeFilter ===  FilterStatus.pending
    ? filteredTasks = tasks.filter(item => !item.isDone)
    : activeFilter === FilterStatus.done
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

  function setFilter(filter) {
    activeFilter = filter
  }
</script>

<main>

<div class="flex flex-col gap-10 items-center">
<span class=" font-bold">Svelte TypeScript To Do List</span>
<div class="flex flex-row gap-2">
{#each filters as filter}
<Button isActive={activeFilter === filter} on:click={() => setFilter(filter)} label={filter}></Button>
{/each}
</div>
<div class="tasks flex flex-col w-full">
{#each filteredTasks as task}
  <li class="task flex flex-row justify-between items-center mx-10">
  <div>
  <input 
  
  bind:checked={task.isDone} 
  type="checkbox"
  on:changed={(event) => task.iDone = event.target.checked}
  >
  <span  class:done={task.isDone}>{task.name}</span>
  </div>
  <Button on:click={() => deleteTask(task)} icon='faTrash'>
  
  </Button>
  </li>
{/each}
</div>
<div>
 <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
        
      </label>
      <input bind:value={newTask} class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Task Name">
</div>
<Button on:click={addTask} label="Add Task"></Button>
</div>
</main>

<style>
  
  .tasks {

  }

  .task {
    list-style: none;
  }

  .done {
    text-decoration: line-through;
  }
</style>