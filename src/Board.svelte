<script>
    import { onMount } from "svelte";
    import Hexagon from "./Hexagon.svelte";
    export let letters = "ONZSEMUACDFNKERUWYE";
    const rows = [
        letters.substring(0, 3),
        letters.substring(3, 7),
        letters.substring(7, 12),
        letters.substring(12, 16),
        letters.substring(16),
    ];

    let swipeActive = false;
    let activeSpaces = [];
    let currHex = null;
    let activeWord = "";
    let lastWord = "";

    function handleWordEnter() {
        swipeActive = true;
        const thishex = this.querySelectorAll(".tile:active")[0];
        // console.log(thislet);
        const thislet = thishex.innerText;
        const thiscoord = thishex.getAttribute("coordinate");
        currHex = thiscoord;

        activeWord = thislet;
        activeSpaces = [coordToSpace(thiscoord)];
    }

    function handleWordExit() {
        swipeActive = false;
        lastWord = activeWord;
        activeWord = "";
        this.querySelectorAll(".tile").forEach((element) => {
            element.classList.remove("wordpart");
            element.classList.remove("errored");
        });
    }

    function getkValue(i, j) {
        const k = i > 2 ? j - 5 : j - 3 - i;
        return k;
    }

    function isAdjacent(coordA, coordB) {
        console.log(`c ${coordA} - ${coordB}`);
        if (coordA === coordB) {
            console.log(" adjacent false: same square");
            return false;
        }
        for (let n = 0; n < 3; n++) {
            console.log(`comp ${n}: ${coordA[n] - coordB[n]}`);
            if (Math.abs(coordA[n] - coordB[n]) > 1) {
                console.log(" adjacent false: two plus");
                return false;
            }
        }
        console.log(" adjacent true");
        return true;
    }

    function coordToSpace(coordStr) {
        const coord = parseCoord(coordStr);
        const starts = {
            0: 0,
            1: 3,
            2: 7,
            3: 12,
            4: 16,
        };
        return starts[coord[0]] + coord[1];
    }

    function parseCoord(coordStr) {
        return coordStr.split(",").map((e) => {
            return parseInt(e);
        });
    }

    let addToWord;
    onMount(() => {
        addToWord = (coordStr) => {
            const coord = parseCoord(coordStr);
            const currHexCoord = parseCoord(currHex);
            console.log("coord");
            console.log(coordStr);
            const space = coordToSpace(coordStr);
            console.log("space");
            console.log(space);
            if (
                !activeSpaces.includes(space) &&
                isAdjacent(coord, currHexCoord)
            ) {
                activeSpaces.push(space);
                activeWord = activeWord + letters[space];
                currHex = coord.join();
                document
                    .querySelectorAll(`.tile[coordinate="${currHex}"]`)[0]
                    .classList.add("wordpart");
            } else if (activeSpaces.includes(space)) {
                document
                    .querySelectorAll(`.tile[coordinate="${currHex}"]`)[0]
                    .classList.add("errored");
            }
        };
    });
    /*
    var handleTouchstart = function(evt) {
		// Store the first Y position of the touch
		startY = evt.touches ? evt.touches[0].screenY : evt.screenY;
	};

	var enable = function() {
		// Listen to a couple key touch events
		window.addEventListener('touchstart', handleTouchstart, supportsPassiveOption ? { passive : false } : false);
		window.addEventListener('touchmove', handleTouchmove, supportsPassiveOption ? { passive : false } : false);
		enabled = true;
	};

	var disable = function() {
		// Stop listening
		window.removeEventListener('touchstart', handleTouchstart, false);
		window.removeEventListener('touchmove', handleTouchmove, false);
		enabled = false;
	};

	var isEnabled = function() {
		return enabled;
	};
    */
</script>

<!-- {@debug currHex} -->
<div class="layout" on:mousedown={handleWordEnter} on:mouseup={handleWordExit}>
    {#each rows as row, i}
        <div class="boardrow" style="transform: translateY({-16 * i}px);">
            {#each row as letter, j}
                <Hexagon
                    char={letter}
                    coordinate="{i},{j},{getkValue(i, j)}"
                    on:mouseover={() => {
                        if (swipeActive) {
                            addToWord(`${i},${j},${getkValue(i, j)}`);
                        }
                    }}
                />
            {/each}
        </div>
    {/each}
    <p>Drag word is {activeWord}</p>
    <p>Last word is {lastWord}</p>
</div>

<style>
    .layout {
        position: relative;
        width: 1200px;
        height: 800px;
        border: solid gray 10px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .boardrow {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 2px;
    }
</style>
