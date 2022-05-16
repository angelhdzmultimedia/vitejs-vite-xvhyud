<script>
export let label = 'Default'
export let icon = null
import * as icons from '@fortawesome/free-solid-svg-icons'
import Fa from 'svelte-fa'
import { createEventDispatcher } from 'svelte';

export let isActive = false
export let color = 'bg-blue-500'
let colors = {
  dark: {
    active: 'active:bg-blue-800',
    hover: 'hover:bg-blue-800'
  },
  normal: {
    active: 'active:bg-blue-500',
    hover: 'hover:bg-blue-500'
  }
}
let normalColor = `${color} ${colors.dark.hover}`
let activeColor = 'bg-green-600 hover:bg-green-800 focus:bg-green-800 active:bg-green-600'
const emit = createEventDispatcher()
</script>
<main>
<button class:active={isActive} on:click={() => emit('click')} 
class="{isActive ? activeColor : normalColor}  text-white font-bold py-2 px-4 rounded">
{#if icon === null}
  {label}
  {:else}
  <Fa icon={icons[icon]}/>
{/if}
</button>
</main> 

<style>

</style>