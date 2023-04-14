<script>
  import Input from "./lib/Input.svelte";
  import { writable } from "svelte/store";

  const userInputStore = writable([]);
  let userInput = [];

  userInputStore.subscribe(value => {
    userInput = value;
  })

  let decode = false;
</script>

<h1 style="margin: 10px;">Germanikus</h1>

{#each userInput as letter}
  <h1>{letter}</h1>
{/each}

<label>
  <Input userInputStore />
  Decode
  <input type="checkbox" bind:checked={decode}>
</label>

<style>
</style>