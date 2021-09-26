<script>
   import { createEventDispatcher } from 'svelte';

   const dispatch = createEventDispatcher();

   let values = {'str': 8, 'dex': 8, 'wis': 8, 'int': 8, 'cha': 8};
   const costs = {8: 0, 9: 1, 10: 2, 11: 3, 12: 4, 13: 5, 14: 7, 15: 9};

   if (localStorage.getItem("abilities") != null) {
      values = JSON.parse(localStorage.getItem("abilities"));
   }

   const handleChange = (ability) => {
      if (values[ability] >= 15) {
         values[ability] = 15;
      }

      if (values[ability] < 8) {
         values[ability] = 8;
      }

      let nums = Object.values(values);
      let points = 28;

      for (var i = 0; i < nums.length; i++) {
         points = points - costs[nums[i]];
      }

      console.log(points)

      if (points < 0) {
         points = 0;
      }

      if (points == 0) {
         if (values[ability] == 8) {
            values[ability] = values[ability] +1;
         }
         else {
            values[ability] = values[ability] -1;
         }
      }

      localStorage.setItem("abilities", JSON.stringify(values));
      dispatch('changed', {val: values, prop: "stats"})
   }
</script>

{#each Object.keys(values) as ability}
   <input type="number" id={ability} bind:value={values[ability]} on:change={() => handleChange(ability)} placeholder={ability}/>
{/each}

<br>

{#each Object.keys(values) as ability}
   <label for="">{ability}</label>
{/each}

<style>
   input {
      height: 75px;
      width: 75px;
      text-align: center;
      margin: 5px;
   }

   label {
      margin-top: 10px;
      margin-left: 30px;
      margin-right: 30px;
      display: inline-block;
   }
</style>