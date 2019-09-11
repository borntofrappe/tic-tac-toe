<script>
  import { fade } from 'svelte/transition';
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  // choice is received from the parent component to describe the initial choice
  export let choice;
  // toggle choice allows to alternate between the two signs
  const toggleChoice = () => choice = choice === 'x' ? 'o' : 'x';

  // array describing the contents of the grid (x, o, '')
  let grid = Array(9).fill('');
  // array describing the 9 buttons (to later access the elements in case of a victory/tie)
  let elements = Array(9);
  // variable dictating a class of .gameover on the grid container (to hide the container before the element is actually removed in favor of the form)
  let gameover = false;
  // describe the winning combinations, through the indexes of adjacent signs
  const combinations = [
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8],
		[2, 4, 6],
  ];

  // function checking for a victory and returning the indexes of the winning items or false
  const checkVictory = () => {
    // loop through the winning combinations
    for(let combination of combinations) {
      // check if the values of the grid at the specified index match
      // ! check immediately if the value is not an empty string
      const [a, b, c] = combination;
      if(grid[a] && grid[a] === grid[b] && grid[a] === grid[c]) {
        return [a, b, c];
      }
    }
    return false;
  }
  // function checking for a tie
  // if there are no longer empty strings
  const checkTie = () => !grid.includes('');

  // function following a click on the grid's button
  const selectCell = (index) => {
    // update the grid with the current choice
    grid = [...grid.slice(0, index), choice, ...grid.slice(index + 1)];
    // check for a victory
    if(checkVictory()) {
      // dispatch the finish event to return to the game component
      dispatch('finish');
      // highlight the winning buttons by reducing the opacity svg elements nested in the buttons which do not represent the winning combination
      const [a, b, c] = checkVictory();
      elements.forEach((element, index) => {
        const node = element.childNodes[0];
        if(node.nodeType === 1 && ![a, b, c].includes(index)) {
          node.style.opacity = 0.2;
        }
      });
      // populate the grid to avoid clicking on other elements
      grid = grid.map(cell => cell ? cell : ' ');
      // set gameover to true to conceal the grid after a brief delay
      gameover = true;
    } else if(checkTie()) {
      // check for tie
      // dispatch the finish event
      dispatch('finish');
      // reduce the opacity of all signs
        console.log(elements);
      elements.forEach(element => {
        const node = element.childNodes[0];
        if(node.nodeType === 1) {
          node.style.opacity = 0.2;
        }
      })
      // set gameover to true to conceal the grid after a brief delay
      gameover = true;
    } else {
      // no victory, no tie, toggle the sign
      toggleChoice();
    }
  }
</script>

<style>
  /* style the grid to show the buttons in three columns and rows */
  .grid {
    max-width: 300px;
    display: flex;
    flex-wrap: wrap;
  }
  /* as the class of .gameover is added, transition the grid out of sight */
  .grid.gameover {
    transition: opacity 0.2s ease-out;
    /* delay to have the grid disappear as the gameover is perceived and before the element is actually removed in favor of the form */
    transition-delay: 3s;
    opacity: 0;
  }
  @supports (display: grid) {
    .grid {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-auto-rows: 100px;
      grid-gap: 0;
    }
    .grid button {
      width: 100%;
      height: 100%;

    }
  }
  .grid button {
    background: none;
    display: block;
    width: 100px;
    height: 100px;
    border: none;
    position: relative;
    color: hsl(53, 95%, 53%);
    padding: 0.5rem;
    overflow: hidden;
  }
  /* include solid borders between the central options */
  .grid button:nth-of-type(3n - 1) {
    border-right: 0.5rem solid currentColor;
    border-left: 0.5rem solid currentColor;
  }
  .grid button:nth-of-type(4),
  .grid button:nth-of-type(5),
  .grid button:nth-of-type(6) {
    border-top: 0.5rem solid currentColor;
    border-bottom: 0.5rem solid currentColor;
  }
  /* show a semitransparent background on hover/focus */
  .grid button:before {
    content: '';
    position: absolute;
    width: 200px;
    height: 200px;
    border-radius: 50%;
    background: currentColor;
    top: 50%;
    left: 50%;
    opacity: 1;
    transform: translate(-50%, -50%) scale(0);
  }
  .grid button:disabled:before {
    display: none;
  }
  .grid button:hover:before,
  .grid button:focus:before {
    transition: all 1.5s cubic-bezier(0.215, 0.61, 0.355, 1);
    opacity: 0.25;
    transform: translate(-50%, -50%) scale(1);
  }
  .grid button svg {
    display: block;
    width: 100%;
    height: 100%;
    /* transition for the change in opacity */
    transition: opacity 0.2s ease-out;
  }
</style>

<div class="grid" in:fade class:gameover>
  <!-- for each item of the grid add a button
  - binding the button to one of the variables in the elements array
  - disabled if the button contains something
  - calling the selectCell function on click
  - displaying the x and o signs to match the possible value
  -->
  {#each grid as cell, i}
    <button bind:this={elements[i]} disabled={cell} on:click={() => selectCell(i)}>
      {#if cell}
        {#if cell === 'x'}
        <svg viewBox="0 0 52 52" width="52" height="52">
          <g transform="translate(26 26)">
            <g transform="rotate(45)">
              <use href="#x"></use>
            </g>
          </g>
        </svg>
        {:else if cell === 'o'}
        <svg viewBox="0 0 52 52" width="52" height="52">
          <g transform="translate(26 26)">
            <use href="#o"></use>
          </g>
        </svg>
        {/if}
      {/if}
    </button>
  {/each}
</div>