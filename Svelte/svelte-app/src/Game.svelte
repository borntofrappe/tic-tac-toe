<script>
  import Form from './Form.svelte';
  import Grid from './Grid.svelte';

  let choice;
  function handleSelection(e) {
    choice = e.detail;
  }
  function handleFinish() {
    const timeout = setTimeout(() => {
      choice = null;
      clearTimeout(timeout);
    }, 3000)
  }
</script>

{#if choice}
  <Grid {choice} on:victory={handleFinish} on:tie={handleFinish} />
{:else}
  <Form on:selection={handleSelection} />
{/if}
