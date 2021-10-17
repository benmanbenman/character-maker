<script>
   import Tabs from './components/shared/Tabs.svelte'
   import Select from './components/Select.svelte'
   import Abilities from './components/Abilities.svelte'

   let items = ['stats', 'slots', 'health', 'traits'];
   let activeItem;

   if (localStorage.getItem('tab_active') == null) {
      activeItem = 'stats';
   }
   else {
      activeItem = localStorage.getItem('tab_active');
   }

   let character = {
      stats: {},
      traits: {},
      slots: {},
      health: {max: 0, current: 0}
   };

   if (localStorage.getItem('character') != null) {
      character = JSON.parse(localStorage.getItem('character'));
   }

   const tabChange = (e) => {
      activeItem = e.detail;
      localStorage.setItem('tab_active', activeItem);
   }

   const changeCharacter = (e) => {
      character[e.detail.prop] = e.detail.val;
      localStorage.setItem('character', JSON.stringify(character));
      console.log(character);
   }

</script>

<main>
   <Tabs {items} {activeItem} on:tabChange={tabChange}/>
   {#if activeItem === 'stats'}
      <p>roll stats.</p>
      <Abilities on:changed={changeCharacter}/>
   {:else if activeItem === 'slots'}
      <p>choose and roll for equipment.</p>
      <Select arr={["",""]} />
   {:else if activeItem === 'health'}
      <p>roll health details.</p>
   {:else if activeItem === 'traits'}
      <p>invent or roll appearance, name etc.</p>
   {/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
	}
</style>