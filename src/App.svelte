<script>
  import Input from "./lib/Input.svelte";
  import Info from "./lib/Info.svelte";
  import Keyboard from "./lib/Keyboard.svelte";
  import { userInputStore, decodeStore } from "./stores";
  import { toGermanikus, fromGermanikus } from "./consts/germanikus";
  import { blur } from "svelte/transition";

  let isTouchDevice = "ontouchstart" in window || navigator.maxTouchPoints > 0;

  let userInput = [];

  userInputStore.subscribe(value => {
    userInput = value;
  })

  $: userInput, convert()

  let decodeInput = false;
  $: decodeStore.set(decodeInput)

  let output = [];
  let convert = () => {
      let dict = (!decodeInput ? toGermanikus : fromGermanikus)
      output = []
      for (const letter of userInput) {
          output.push(
              (letter in dict ? dict[letter] : letter)
          );
      }
  };

</script>

<Info />

<div class="content">
<h1 style="margin: 10px;">Germanikus Cipher</h1>

<label>
  <Input />
  Decode
  <input type="checkbox" bind:checked={decodeInput}>
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
</div>

{#if !isTouchDevice}
<a class="source-link" href="http://github.com/grishatop1/germanikus-svelte" target="_blank">
  <img src="/src/assets/gh.svg" alt="See the source on Github!" height="25">
</a>
{:else}
  <Keyboard />
{/if}



<style>
  .content {
    margin-bottom: 50px;
  }
  .output-letter {
    font-size: 3em;
  }
  .source-link {
    color: white;
  }
</style>
