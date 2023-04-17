<script>
  import Input from "./lib/Input.svelte";
  import Info from "./lib/Info.svelte";
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

</script>

<Info />

<h1 style="margin: 10px;">Germanikus Cipher</h1>

<label>
  <Input onChange={convert} />
  Decode
  <input type="checkbox" bind:checked={decode} on:change={convert}>
</label>

<p style="font-size:small; font-style:italic">Doesn't work on mobile yet, sorry for that!</p>

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
