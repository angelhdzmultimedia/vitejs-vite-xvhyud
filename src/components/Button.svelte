<script>
export let label = 'Default'
export let icon = null
import * as icons from '@fortawesome/free-solid-svg-icons'
import Fa from 'svelte-fa'
import { createEventDispatcher } from 'svelte';

const emit = createEventDispatcher()
</script>
<main>
<button on:click={() => emit('click')} class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
{#if icon === null}
  {label}
  {:else}
  <Fa icon={icons[icon]}/>
{/if}
</button>
</main> 