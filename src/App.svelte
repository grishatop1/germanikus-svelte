<script>
  import Input from "./lib/Input.svelte";
  import Info from "./lib/Info.svelte";
  import Keyboard from "./lib/Keyboard.svelte";
  import Checkbox from "./lib/Checkbox.svelte";
  import Convert from "./lib/Convert.svelte";
  import { fade } from "svelte/transition";

  let isTouchDevice = "ontouchstart" in window || navigator.maxTouchPoints > 0;
  let output = [];

</script>

<div class="content">
<h1 style="margin: 10px;">Germanikus Cipher</h1>

<Convert bind:output/>
<Info />
<Input />
<Checkbox />

<div class="output-letter">
  {#each output as letter}
    <span transition:fade>{letter}</span>
  {/each}
  <span id="placeholder">
    {#if output.length == 0}
      &ZeroWidthSpace;
    {/if}
  </span>
</div>
</div>

<a class="source-link" href="http://github.com/grishatop1/germanikus-svelte" target="_blank">
  <img src="/src/assets/gh.svg" alt="See the source on Github!" height="25">
</a>
{#if isTouchDevice}
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
    font-weight: bold;
    position: absolute;
    top: 20px;
    left: 30px;
    font-size: 1.5em;
    user-select: none;
  }
</style>
