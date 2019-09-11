<!-- component describing the tic-tac-toe game, from selection to grid -->
<script>
  // component describing the form to select between x and o
  import Form from './Form.svelte';
  // component describing the 3x3 grid to play the actual game
  import Grid from './Grid.svelte';

  // choice describes the choice between x and o
  // the variable is set according to the value received from the form component
  let choice;
  function handleSelection(e) {
    choice = e.detail;
  }

  // choice is explicitly set to null following the event dispatched by the grid
  // this makes it possible to show the form component once more
  function handleFinish() {
    const timeout = setTimeout(() => {
      choice = null;
      clearTimeout(timeout);
    }, 3000)
  }
</script>

{#if choice}
  <!-- finish is dispatched by the grid as a victory/tie is reached -->
  <Grid {choice} on:finish={handleFinish} />
{:else}
  <!-- selection is dispatched by the form following a selection -->
  <Form on:selection={handleSelection} />
{/if}
