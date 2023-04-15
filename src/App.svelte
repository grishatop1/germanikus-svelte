<script>
  import Input from "./lib/Input.svelte";
  import { userInputStore } from "./stores";
  import { toGermanikus, fromGermanikus } from "./consts/germanikus";
  import { blur } from "svelte/transition";

  const src = "/src/assets/gh.svg";
  const alt = "See the source on Github!";
  const href = "http://github.com/grishatop1/germanikus-svelte"

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
          );
      }
  };

  let panelVisible = false;
  let handleInfoPanel = () => {
    panelVisible = !panelVisible;
  }

</script>
<p class="info-trigger" on:mousedown={handleInfoPanel}>
  what's germanikus?
</p>

{#if panelVisible}
<div class="info-panel">
  asd
</div>
{/if}

<h1 style="margin: 10px;">Germanikus</h1>

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

<a class="source-link" {href} target="_blank">
  <img {src} {alt} title={alt} height="25">
</a>

<style>
  .info-trigger {
    color: #70707a;
    font-weight: bold;
    display: flex;
    position: fixed;
    top: 1%;
    right: 2%;
    cursor: pointer;
  }
  .info-panel {
    display: flex;
    position: relative;
    top: 1%;
    left: 2%;
    display: none;
  }
  .output-letter {
    font-size: 3em;
  }
  .source-link {
    color: white;
    display: flex;
    position: fixed;
    bottom: 5%;
  }
</style>