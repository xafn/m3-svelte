<script>
	import Switch from '$lib/Switch/Switch.svelte';
</script>

<main class="wrapper">
	<h1>Material 3 Svelte</h1>
	<p>Svelte UI component library for Google's Material 3.</p>

	<div class="label-large">Switch</div>
	<Switch />
</main>

<style>
	[class*='label-'] {
		margin-bottom: 0.5rem;
	}
</style>
