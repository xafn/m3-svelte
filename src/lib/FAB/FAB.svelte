<script lang="ts">
	import Svg from '$lib/SVG/Svg.svelte';

	/**
	 * Specify the type of FAB
	 * @type {"default" | "small" | "large"}
	 */
	export let type = 'default';
	export let icon = '';

	const iconSizes = {
		default: 24,
		small: 24,
		large: 36
	};
</script>

<button on:click class="fab-{type}">
	<span class="tint" />
	<div class="slot">
		<Svg viewBoxHeight={48} svgHeight={iconSizes[type]}>
			<path d={icon} />
		</Svg>
	</div>
</button>

<style lang="scss">
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
	}

	.fab-default {
		height: 56px;
		width: 56px;
		border-radius: 16px;
		padding: 16px;
		background-color: var(--md-sys-color-primary-container);

		path {
			fill: var(--md-sys-color-on-primary-container);
		}
	}

	.fab-small {
		height: 40px;
		width: 40px;
		border-radius: 12px;
		padding: 12px;
		background-color: var(--md-sys-color-primary-container);

		path {
			fill: var(--md-sys-color-on-primary-container);
		}
	}

	.fab-large {
		height: 96px;
		width: 96px;
		border-radius: 28px;
		padding: 28px;
		background-color: var(--md-sys-color-primary-container);

		path {
			fill: var(--md-sys-color-on-primary-container);
		}
	}
</style>
