<script>
  import Form from './Form.svelte';
  // import Grid from './Grid.svelte';

  let choice;
  function handleSelection(e) {
    choice = e.detail;
  }
</script>

{#if choice}
  <!-- <Grid {choice} /> -->
{:else}
  <Form on:selection={handleSelection} />
{/if}
