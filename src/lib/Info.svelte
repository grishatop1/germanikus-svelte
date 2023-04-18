<script>
  import { slide } from "svelte/transition";

  let panelVisible = false;
</script>

<div class="info">
  <div class="info-trigger" on:mousedown={() => {panelVisible = !panelVisible;}}>
    {#if !panelVisible}
      what's germanikus?
    {:else}
      hide
    {/if}
  </div>
  {#if panelVisible}
    <div class="info-panel" transition:slide on:mousedown={() => {panelVisible = false;}}>
      Germanikus is a basic substitution cipher, where the letters of the
      codeword "germanikus" are replaced with numbers, in accordance with this
      table:
      <pre class="info-pre">
        germanikus
        1234567890
      </pre>
      And in some sources:
      <pre class="info-pre">
        germanikus
        0123456789
      </pre>
      The letters not found in the codeword are simply written as they are.
    </div>
  {/if}
</div>

<style>
  .info-trigger {
    color: #818189;
    font-weight: bold;
    position: absolute;
    top: 20px;
    right: 30px;
    cursor: pointer;
    font-size: 1.5em;
    user-select: none;
  }
  .info-panel {
    display: flex;
    flex-direction: column;
    position: absolute;
    background-color: #303038;
    top: 75px;
    padding: 20px;
    right: 20px;
    max-width: 350px;
    cursor: pointer;
    border-radius: 20px;
    color: white;
    font-size: 15px;
    font-weight: bold;
    text-align: center;
    word-wrap: break-word;
    overflow: scroll;
  }
  .info-pre {
    font-weight: bold; 
    font-size: 17px;
    white-space: pre-line;
  }

  @media (max-width: 450px) {
    .info-panel {
      left: 50%;
      transform: translateX(-50%);
      width: 80%;
    }
  }
</style>
