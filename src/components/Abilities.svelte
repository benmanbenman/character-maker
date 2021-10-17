<script>
   import { onMount } from 'svelte';
   import { createEventDispatcher } from 'svelte';

   const dispatch = createEventDispatcher();

   let values = {'str': 1, 'dex': 1, 'con': 1, 'wis': 1, 'int': 1, 'cha': 1};

   if (localStorage.getItem("abilities") != null) {
      values = JSON.parse(localStorage.getItem("abilities"));
   };

   console.log(localStorage.getItem("set"));

   const handleChange = (ability) => {
      localStorage.setItem("abilities", JSON.stringify(values));
      dispatch('changed', {val: values, prop: "stats"});
      localStorage.setItem("set", true);
   };
   
   const randomise = () => {
      var keys = Object.keys(values) 
      for (var i = 0; i < keys.length; i++) {
         var lowest = 6;
         for (var j = 0; j < 3; j++) {
            var num = Math.floor(Math.random() * 7);
            if (num == 0) {
               num = 1
            }
            if (num < lowest) {
               lowest = num;
            };
         };
         values[keys[i]] = lowest;
         handleChange(keys[i]);
      }
   };
</script>

{#each Object.keys(values) as ability}
   <input type="number" id={ability} bind:value={values[ability]} placeholder={ability} readonly/>
{/each}

<br>

{#each Object.keys(values) as ability}
   <label for="{ability}">{ability}</label>
{/each}

<br>

{#if localStorage.getItem("set") == null}
   <button on:click|once={randomise} id="roll">
      roll
   </button>
{/if}

<style>
   input {
      height: 75px;
      width: 75px;
      text-align: center;
      margin: 5px;
   }

   /* center input text */

   input[type='number']::-webkit-inner-spin-button, 
   input[type='number']::-webkit-outer-spin-button { 
      -webkit-appearance: none;
      margin: 0;
   }

   label {
      margin-top: 10px;
      margin-left: 30px;
      margin-right: 30px;
      display: inline-block;
   }

   button {
      margin-top: 30px;
   }
</style>