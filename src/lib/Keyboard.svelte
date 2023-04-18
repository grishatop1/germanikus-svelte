<script>
    import { onMount } from "svelte";
    import { userInputStore, decodeStore } from "../stores";

    let decode = false;
    

    let generateKeyboard = () => {
        document.getElementById("keyboard").innerHTML = "";
        let order = [];
        if (decode) {
            order = [
                ["1", "2", "3", "4", "5"],
                ["6", "7", "8", "9", "0"],
                ["space", "backspace"],
            ];
        } else {
            order = [
                ["q", "w", "e", "r", "t", "y", "u", "i", "o", "p"],
                ["a", "s", "d", "f", "g", "h", "j", "k", "l"],
                ["z", "x", "c", "v", "b", "n", "m", "backspace"],
                ["space"],
            ];
        }
        let keyboard = document.getElementById("keyboard");
        let row;
        let button;
        for (let i = 0; i < order.length; i++) {
            row = document.createElement("div");
            row.className = "keyrow";
            for (let j = 0; j < order[i].length; j++) {
                button = document.createElement("button");
                if (order[i][j] === "space" && !decode) {
                    button.style.width = "100%";
                }
                button.innerHTML = order[i][j];
                button.className = "tipka disable-dbl-tap-zoom user-select-none";
                button.setAttribute("tabindex", "-1");
                row.appendChild(button);
                button.onclick = function () {
                    userInputStore.update((current) => {
                        // @ts-ignore
                        if (this.innerHTML == "backspace") {
                            // @ts-ignore
                            current.pop();
                            //@ts-ignore
                        } else if (this.innerHTML == "space") {
                            current.push(" ");
                        } else {
                            // @ts-ignore
                            current.push(this.innerHTML);
                        }
                        return current;
                    });
                };
            }
            keyboard.appendChild(row);
        }
    };

    onMount(() => {
        generateKeyboard();
        decodeStore.subscribe((value) => {
            decode = value;
            generateKeyboard();
        });
    });
</script>

<div id="keyboard" />

<style>
    #keyboard {
        position: fixed;
        bottom: 5px;
        width: 97%;
        max-width: 320px;
    }
</style>
