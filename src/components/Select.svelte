<script>
	import { createEventDispatcher } from 'svelte';

   const dispatch = createEventDispatcher();

   export let arr = [];
   export let value;
   export let storage;
   export let prop;

   if (localStorage.getItem(storage) != null) {
      value = localStorage.getItem(storage)
   }

   const handleClick = () => {
      localStorage.setItem(storage, value)
      dispatch('changed', {val: value, prop: prop});
   }
</script>

<select name="" bind:value on:change={handleClick}>
   <option value="" disabled selected>Select</option>
   {#each arr as item}
      <option value={item}>{item}</option>
      <br>
   {/each}
</select>