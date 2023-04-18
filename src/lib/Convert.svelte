<script>
  import { toGermanikus, fromGermanikus } from "../consts/germanikus";
  import { userInputStore, decodeStore } from "../stores";

  let userInput = [];
  userInputStore.subscribe(value => {
    userInput = value;
  })

  let decodeInput = false;
  decodeStore.subscribe(value => {
    decodeInput = value;
  })

  export let output = [];
  let convert = () => {
      let dict = (!decodeInput ? toGermanikus : fromGermanikus)
      output = []
      for (const letter of userInput) {
          output.push(
              (letter in dict ? dict[letter] : letter)
          );
      }
  };

  $: userInput, convert()
  $: decodeInput, convert()

</script>