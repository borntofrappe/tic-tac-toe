<script>
  import { fade } from 'svelte/transition';

  // once a selection is made, dispatch the selection event to inform the parent component of the chosen sign
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  let selection;
  $: if(selection) {
    dispatch('selection', selection);
  }
</script>
<style>
  form {
    display: flex;
  }
  form div {
    position: relative;
  }
  form div svg {
    display: block;
    width: 175px;
    height: auto;
  }
  form div input {
    position: absolute;
    width: 100%;
    height: 100%;
    opacity: 0;
  }
  /* absolute position the separator line in the center of the div */
  form svg#separator {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    height: 300px;
    width: auto;
  }
</style>

<!-- in a form display two options side by side -->
<form>
  <div>
    <input type="radio" bind:group={selection} value="x" id="x" name="x" />
    <label for="x">
      <!-- use the svg shapes used in the loader
      ! while the shapes are 52x52, specify a viewBox which is half wide as the viewBox of the loader
      this to maintain the spacing between the signs
      -->
      <svg viewBox="0 0 72 52" width="72" height="52">
        <g transform="translate(26 26)">
          <g transform="rotate(45)">
            <use href="#x"></use>
          </g>
        </g>
      </svg>
    </label>
  </div>
  <!-- line separating the two options
  made to fade in
  -->
  <svg in:fade id="separator" viewBox="0 0 2 100" width="6" height="300">
    <path d="M 1 0 v 100" fill="none" stroke="currentColor" stroke-width="2"></path>
  </svg>
  <div>
    <input type="radio" bind:group={selection} value="o" id="o" name="o" />
    <label for="o">
      <svg viewBox="0 0 72 52" width="72" height="52">
        <g transform="translate(46 26)">
          <use href="#o"></use>
        </g>
      </svg>
    </label>
  </div>
</form>