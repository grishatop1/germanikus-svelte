<script>
  import { decodeStore } from "../stores";

  let decodeInput = false;
  $: decodeStore.set(decodeInput)
</script>

<label>
  <div class="switch-with-text">
    {#if decodeInput}
    <span>Encode</span>
    {:else}
    <b>Encode</b>
    {/if}
    <div class="switch">
      <div class="container">
        <input class="checkbox" type="checkbox" bind:checked={decodeInput}>
        <div class="slider round"></div>
      </div>
    </div>
    {#if !decodeInput}
    <span>Decode</span>
    {:else}
    <b>Decode</b>
    {/if}
  </div>
</label>

<style>
  b, span {
    width: 50px;
  }
.switch-with-text {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-top: 15px;
  }
  .switch-with-text * {
    margin: 0px 9px;
  }
  .switch {
    display: inline-block;
    height: 28px;
    position: relative;
    width: 70px;
  }
  .switch input {
    display:none;
  }
  .slider {
    background-color: #fffd;
    bottom: 0;
    cursor: pointer;
    left: 0;
    position: absolute;
    right: 0;
    top: 0;
    transition: .4s;
  }
  .slider:before {
    background-color: #24242a;
    bottom: 4px;
    content: "";
    height: 20px;
    left: 4px;
    position: absolute;
    transition: .1s;
    width: 20px;
  }
  input:checked + .slider {
    background-color: #fffd;
  }
  input:checked + .slider:before {
    transform: translateX(24px);
  }
  .slider.round {
    border-radius: 34px;
  }
  .slider.round:before {
    border-radius: 50%;
  }
</style>