<script>
   import { createEventDispatcher } from "svelte";

   const dispatch = createEventDispatcher()

   export let items;
   export let activeItem;
</script>

<div class="tabs">
   <ul>
      {#each items as item}
         <li on:click={() => dispatch('tabChange', item)}>
            <div class:active={item === activeItem}>{item}</div>
         </li>
      {/each}
   </ul>
</div>

<style>
   .tabs {
      margin-bottom: 40px;
   }

   ul {
      display: flex;
      justify-content: center;
      padding: 0;
      list-style: none;
   }

   li {
      margin: 0 16px;
      font-size: 18px;
      color: #0D0A0B;
      cursor: pointer;
   }

   .active {
      color: #AD2831;
      border-bottom: 2px solid #AD2831;
      padding-bottom: 8px;
   }
</style>