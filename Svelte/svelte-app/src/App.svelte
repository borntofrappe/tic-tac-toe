<script>
	import SVG from './SVG.svelte';
	import Loader from './Loader.svelte';
	import Game from './Game.svelte';

	let isLoading = true;

	function handleIteration() {
		isLoading = false;
	}
</script>

<SVG />

{#if isLoading}
	<Loader on:iteration={handleIteration} />
{:else}
	<Game />
{/if}