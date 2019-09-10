<script>
  export let choice;
  let grid = Array(9).fill('');

  const toggleChoice = () => choice = choice === 'x' ? 'o' : 'x';
  const selectCell = (index) => {
    grid = [...grid.slice(0, index), choice, ...grid.slice(index + 1)];
    toggleChoice();
    console.log(choice);
  }
</script>

<style>
  .grid {
    max-width: 300px;
    display: flex;
    flex-wrap: wrap;
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
  }
</style>

<div class="grid">
  {#each grid as cell, i}
    <button disabled={cell} on:click={() => selectCell(i)}>
      {#if cell}
        {#if cell === 'x'}
        <svg viewBox="0 0 52 52" width="52" height="52">
          <g transform="translate(26 26)">
            <g transform="rotate(45)">
              <use href="#x"></use>
            </g>
          </g>
        </svg>
        {:else}
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