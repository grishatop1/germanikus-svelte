<script>
    import { fade } from "svelte/transition";

    export let userInputStore;
    let current = [];
    const re = /[A-Za-z0-9]/

    document.onkeydown = (e) => {
      e.preventDefault()
      if (e.key == "Backspace") current.pop();
      if (e.key == " ") current.push(" ");
      current = current;
      if (!re.test(e.key) || e.key.length != 1) return;
      current.push(e.key);
      userInputStore.set(current);
    }
</script>

<div class="input-container">
  {#if !current.length}
    <span class="default-text">type here</span>
  {/if}
{#each current as letter}
  <span class="letter">{(letter == " ") ? "\u00a0" : letter}</span>
{/each}
<span class="caret"></span>
</div>

<style>
  .input-container {
    display: flex;
    justify-content: center;
    margin-bottom: 10px;
  }
  .caret {
    width: 2px;
    height: 1.5em;
    background-color: white;
    display: inline-block;
    animation: blink 0.5s infinite alternate;
    transform: translateY(7px);
    margin-left: 2px;
  }
  .default-text {
    color: gray;
    font-size: 1.5em;
    font-weight: bold;
  }
  .letter {
    font-size: 1.5em;
    font-weight: bold;
  }

  @keyframes blink {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>