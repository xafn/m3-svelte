<script>
	import ProgressIndicator from '$lib/ProgressIndicator/ProgressIndicator.svelte';
import Switch from '$lib/Switch/Switch.svelte';
</script>

<main class="wrapper">
	<h1>Material 3 Svelte</h1>
	<p>Svelte UI component library for Google's Material 3.</p>

	<div>
	    <div class="label-large">Switch</div>
    	<Switch />
	</div>

    <br/>
    <div>
        <div class="label-large">Progress Indicator</div>
        <ProgressIndicator/>
        <br/>
        <ProgressIndicator value={29}/>
    </div>
</main>

<style>
	[class*='label-'] {
		margin-bottom: 0.5rem;
	}
</style>
