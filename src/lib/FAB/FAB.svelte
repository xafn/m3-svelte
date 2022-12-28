<script lang="ts">
	import Svg from '$lib/SVG/Svg.svelte';

	/**
	 * Specify the type of FAB.
	 * @type {"default" | "small" | "large" | "extended"}
	 */
	export let type = 'default';
	export let icon = '';

	const iconSizes = {
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
	<Fab
		type="extended"
		icon="M39.8 14.95 33.25 8.4l2-2q.95-.95 2.325-.925 1.375.025 2.375.975l1.9 1.85q1 1 .925 2.35-.075 1.35-1.025 2.3ZM37.7 17 12.35 42.35h-6.5v-6.5l25.3-25.35Z"
	>
		Edit
	</Fab>
```
***
[M3 FAB guidelines](https://m3.material.io/components/floating-action-button/guidelines)  
[M3 Extended FAB guidelines](https://m3.material.io/components/extended-fab/guidelines)
-->
<button on:click class="fab-{type}">
	<span class="tint" />
	<div class="slot">
		<Svg viewBoxHeight={48} svgHeight={iconSizes[type]}>
			<path d={icon} />
		</Svg>
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
		gap: 8px;
	}

	.extended-text {
		@include label-large;
		color: var(--md-sys-color-on-primary-container);
	}

	[class*='fab-'] {
		background-color: var(--md-sys-color-primary-container);

		path {
			fill: var(--md-sys-color-on-primary-container);
		}
	}

	.fab-default {
		height: 56px;
		width: 56px;
		border-radius: 16px;
		padding: 16px;
	}

	.fab-small {
		height: 40px;
		width: 40px;
		border-radius: 12px;
		padding: 12px;
	}

	.fab-large {
		height: 96px;
		width: 96px;
		border-radius: 28px;
		padding: 28px;
	}

	.fab-extended {
		height: 56px;
		min-width: 80px;
		border-radius: 16px;
		padding: 16px;
	}
</style>
