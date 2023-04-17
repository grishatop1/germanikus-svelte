<script>
  import Input from "./lib/Input.svelte";
  import { userInputStore } from "./stores";
  import { toGermanikus, fromGermanikus } from "./consts/germanikus";
  import { blur } from "svelte/transition";

  let userInput = [];

  userInputStore.subscribe(value => {
    userInput = value;
  })

  let decode = false;

  let output = [];
  let convert = () => {
      let dict = (!decode ? toGermanikus : fromGermanikus)
      output = []
      for (const letter of userInput) {
          output.push(
              (letter in dict ? dict[letter] : letter)
          )
      }
  };

</script>

<h1 style="margin: 10px;">Germanikus Cipher</h1>

<label>
  <Input onChange={convert} />
  Decode
  <input type="checkbox" bind:checked={decode} on:change={convert}>
</label>

<div class="output-letter">
  {#each output as letter}
    <span transition:blur>{letter}</span>
  {/each}
  <span id="placeholder">
    {#if output.length == 0}
      &ZeroWidthSpace;
    {/if}
  </span>
</div>

<style>
  .output-letter {
    font-size: 3em;
  }
</style>