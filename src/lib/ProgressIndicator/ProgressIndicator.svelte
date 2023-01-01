<script lang="ts">
	export let value: number | undefined = 0;
	export let max = 100;
</script>

<!-- 
  @component
  **Progress Indicators**  
  Progress indicators inform users about the status of ongoing processes, such as loading 
  an app or submitting a form. There are two types of progress indicators: Linear and circular.
  When no value is passed, the progress bar becomes indeterminate. Due to CSS limitations, 
  indeterminate progress bars do not use semantic HTML `<progress/>` tags.

*** 
**Example usage**   
```tsx
	<ProgressIndicator value={loadingProgress}/>
	<ProgressIndicator/>
```
***
[M3 guidelines](https://m3.material.io/components/progress-indicators/guidelines)  
-->

<!-- It's impossible to animate the value of a progress element as far as I know -->
<svelte:element
	this={!value ? 'div' : 'progress'}
	role="progressbar"
	class="progress"
	{value}
	{max}
>
	<!-- Indeterminate progress value -->
	{#if !value}
		<span class="progress-value" />
		<!-- Second progress value for better animation -->
		<span class="progress-value-2" />
	{/if}
</svelte:element>

<style lang="scss">
	.progress {
		-webkit-appearance: none;
		-moz-appearance: none;
		appearance: none;
		border: 0;
		height: 0.25rem;
		border-radius: 0;
		width: auto;
		position: relative;
		background-color: var(--md-sys-color-surface-variant);
	}

	progress {
		margin: 0;
		display: block;
		&::-webkit-progress-bar {
			background-color: var(--md-sys-color-surface-variant);
		}

		&[value]::-webkit-progress-value {
			background-color: var(--md-sys-color-primary);
		}

		&[value]::-moz-progress-bar {
			background-color: var(--md-sys-color-primary);
		}
	}

	// styling for indeterminate value
	.progress-value,
	.progress-value-2 {
		display: inline-block;
		position: absolute;
		height: 0.25rem;
		background-color: var(--md-sys-color-primary);
	}

	.progress-value {
		animation: inditermate 3s var(--md-sys-motion-easing-standard) 0.5s infinite;
	}

	.progress-value-2 {
		animation: inditermate 3s var(--md-sys-motion-easing-standard) 1s infinite;
	}

	@keyframes inditermate {
		0% {
			width: 0;
			margin-left: 0;
		}
		50% {
			width: 100%;
			margin-left: 0;
		}
		100% {
			width: 0;
			margin-left: 100%;
		}
	}
</style>
