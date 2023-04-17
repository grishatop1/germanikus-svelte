<script>
    import { userInputStore } from "../stores";

    export let onChange = () => {};
    let current = [];
    const re = /[A-Za-z0-9]/

    userInputStore.subscribe((value) => {
      current = value;
    })

    document.onkeydown = (e) => {
      //e.preventDefault()
      if (e.key == "Backspace") current.pop();
      if (e.key == " " && current.length) current.push(" ");
      current = current;
      userInputStore.set(current);
      onChange();
      if (!re.test(e.key) || e.key.length != 1) return;
      current.push(e.key.toLowerCase());
      userInputStore.set(current);
      onChange();
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
    position: relative;
    z-index: -1;
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
    font-weight:lighter;
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
