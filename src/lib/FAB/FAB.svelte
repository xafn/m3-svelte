<script lang="ts">
	import Svg from '$lib/SVG/Svg.svelte';

	/**
	 * Specify the type of FAB.
	 * @type {"default" | "small" | "large" | "extended"}
	 */
	export let type = 'default';
	export let icon = '';

	const iconSizes: { [key: string]: number } = {
		default: 24,
		small: 24,
		large: 36,
		extended: 24
	};
</script>

<!-- 
  @component
  **FABs**  
  The FAB represents the most important action on a screen. It puts key actions within reach. 
  There are four types of floating action buttons: default FAB, small FAB, large FAB, and extended FAB.

*** 
**Example usage**   
```tsx
	<Fab type="extended" icon="warning">
		Edit
	</Fab>
```
***
[M3 FAB guidelines](https://m3.material.io/components/floating-action-button/guidelines)  
[M3 Extended FAB guidelines](https://m3.material.io/components/extended-fab/guidelines)
-->
<button on:click class="fab-{type}" {...$$restProps}>
	<span class="tint" />
	<div class="slot">
		<div style="font-size: {iconSizes[type]}px;" class="icon">{icon}</div>
		{#if type === 'extended'}
			<div class="extended-text"><slot /></div>
		{/if}
	</div>
</button>

<style lang="scss">
	@import '../../styles/typography.module.scss';

	button {
		background-color: transparent;
		margin: 0;
		padding: 0;
		border: none;
		display: flex;
		overflow: hidden;
		position: relative;
		vertical-align: top;
		cursor: pointer;
		align-items: center;
		justify-content: center;
		box-shadow: var(--md-sys-elevation-level3);
	}

	.tint {
		position: absolute;
		display: inline-block;
		pointer-events: none;
		height: 100%;
		width: 100%;
		top: 0;
		left: 0;
		opacity: 0;
		transition: all 0.2s var(--md-sys-motion-easing-standard);
	}

	button {
		.tint {
			background-color: var(--md-sys-color-on-primary-container);
			opacity: 0;
		}

		&:hover .tint {
			opacity: 0.08;
		}
		&:active .tint {
			opacity: 0.16;
		}
	}

	.slot {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 0.5rem;
	}

	.extended-text {
		@include label-large;
		color: var(--md-sys-color-on-primary-container);
	}

	[class*='fab-'] {
		background-color: var(--md-sys-color-primary-container);

		.icon {
			@include icon;
			color: var(--md-sys-color-on-primary-container);
		}
	}

	.fab-default {
		height: 3.5rem;
		width: 3.5rem;
		border-radius: 1rem;
		padding: 1rem;
	}

	.fab-small {
		height: 2.5rem;
		width: 2.5rem;
		border-radius: 0.75rem;
		padding: 0.75rem;
	}

	.fab-large {
		height: 6rem;
		width: 6rem;
		border-radius: 1.75rem;
		padding: 1.75rem;
	}

	.fab-extended {
		height: 3.5rem;
		min-width: 5rem;
		border-radius: 1rem;
		padding: 1rem;
	}
</style>
