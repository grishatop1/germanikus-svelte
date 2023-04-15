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

  let panelVisible = true; //false;

</script>

<div class="info-trigger" on:mousedown={() => {panelVisible = !panelVisible}}>
  what's germanikus?

  {#if panelVisible}
  <div class="info-panel">
  Germanikus is a basic substitution cypher, where
  the letters of the codeword "germanikus" are replaced
  in accordance with this table:
  <pre class="info-pre">
    germanikus
    1234567890
  </pre>
  And in some sources:
  <pre class="info-pre">
    germanikus
    0123456789
  </pre>
  The letters not found in the codeword are simply
  written as they are.
  </div>
  {/if}
</div>


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
    color: #818a9a;
    font-weight: bold;
    display: flex;
    position: fixed;
    top: 3%;
    right: 2%;
    cursor: pointer;
    font-size: 140%;
  }
  .info-panel {
    display: flex;
    flex-direction: column;
    position: fixed;
    background-color: #c1cada;
    width: 26%;
    height: 40%;
    top: 10%;
    right: 2%;

    border-radius: 5%;

    padding: 2%;

    color: #1c1c1e;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
    word-wrap: break-word;
    overflow: scroll;
  }
  .info-pre {
    font-weight: bold;
    font-size: 111%;
    white-space: pre-line;
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