<script>
   import Tabs from './components/shared/Tabs.svelte'
   import Select from './components/Select.svelte'

   let items = ['race', 'class', 'stats', 'details', 'equipment'];
   let activeItem;

   if (localStorage.getItem('tab_active') == null) {
      activeItem = 'race';
   }
   else {
      activeItem = localStorage.getItem('tab_active');
   }


   let character = {
      race: "",
      class: "",
      subclass: "",
      stats: [],
      details: "",
      equipment: []
   };

   const tabChange = (e) => {
      activeItem = e.detail;
      localStorage.setItem('tab_active', activeItem);
   }

   const changeCharacter = (e) => {
      character[e.detail.prop] = e.detail.val;
      console.log(character);
   }
</script>

<main>
   <Tabs {items} {activeItem} on:tabChange={tabChange}/>
   {#if activeItem === 'race'}
      <p>choose race.</p>
      <Select arr={["Dragonborn", "Dwarf", "Elf", "Gnome", "Half-Elf", "Halfling", "Human", "Tiefling"]} storage="race_active" prop="race" on:changed={changeCharacter}/>
   {:else if activeItem === 'class'}
      <p>choose class and subclass.</p>
      <Select arr={["Barbarian", "Bard", "Cleric", "Druid", "Fighter", "Monk", "Paladin", "Ranger", "Rogue", "Sorcerer", "Warlock", "Wizard"]} storage="class_active" prop="class" on:changed={changeCharacter}/>
   {:else if activeItem === 'stats'}
      <p>choose stats.</p>
   {:else if activeItem === 'details'}
      <p>change name, appearance etc.</p>
   {:else if activeItem === 'equipment'}
      <p>choose equipment and gold.</p>
   {/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
	}
</style>