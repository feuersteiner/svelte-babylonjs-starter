<script>
	import Engine from '$lib/engine.svelte';
</script>

<div class="column">
	<h1>Welcome to Babylonjs on Svelte!</h1>
	<Engine />
</div>

<style>
	.column {
		display: flex;
		flex-direction: column;
		gap: 1em;
		width: 100vw;
		height: 100%;
		overflow-y: hidden;
	}
</style>
