<script>
  import { decodeStore } from "../stores";

  let decodeInput = false;
  $: decodeStore.set(decodeInput)
</script>

<label>
  <div class="switch-with-text">
    Encode
    <div class="switch">
      <div class="container">
        <input class="checkbox" type="checkbox" bind:checked={decodeInput}>
        <div class="slider round"></div>
      </div>
    </div>
    Decode
  </div>
</label>

<style>
.switch-with-text {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  }
  .switch-with-text * {
    margin: 0px 10px;
  }
  .switch {
    display: inline-block;
    height: 34px;
    position: relative;
    width: 80px;
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
    height: 26px;
    left: 4px;
    position: absolute;
    transition: .1s;
    width: 26px;
  }
  input:checked + .slider {
    background-color: #fffd;
  }
  input:checked + .slider:before {
    transform: translateX(26px);
  }
  .slider.round {
    border-radius: 34px;
  }
  .slider.round:before {
    border-radius: 50%;
  }
</style>