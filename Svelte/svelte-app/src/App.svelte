<script>
	// defs block describing the shapes used in the project
	import DefsBlock from './DefsBlock.svelte';
	// loader animating the x and o signs
	import Loader from './Loader.svelte';
	// component describing the game
	import Game from './Game.svelte';

	// show the loader, at least until the first iteration of its animation
	let isLoading = false;
	function handleIteration() {
		isLoading = false;
	}
</script>

<DefsBlock />

<!-- iteration is an event dispatched by the svg -->
{#if isLoading}
	<Loader on:iteration={handleIteration} />
{:else}
	<Game />
{/if}