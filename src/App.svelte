<script>
   import Tabs from './components/Tabs.svelte'

   let items = ['stats', 'details'];
   let activeItem = 'stats';

   const tabChange = (e) => {
      activeItem = e.detail;
   }
</script>

<main>
   <Tabs {items} {activeItem} on:tabChange={tabChange}/>
   {#if activeItem === 'stats'}
      <p>test</p>
   {:else if activeItem === 'details'}
      <p>nwe test</p>
   {/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
</style>