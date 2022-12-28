<script>
	import Svg from '$lib/SVG/Svg.svelte';

	/**
	 * Specify the type of button
	 * @type {"elevated" | "filled" | "tonal" | "outlined" | "text" | "snackbar"}
	 */
	export let type = 'filled';
	export let disabled = false;
	export let icon = '';
</script>

<button on:click class="{icon ? 'icon-button' : ''} button-{type}">
	<span class="tint" />

	<div class="slot">
		{#if icon}
			<Svg viewBoxHeight={48} svgHeight={18}>
				<path d={icon} />
			</Svg>
		{/if}

		<slot />
	</div>
</button>

<style lang="scss">
	@import '../../styles/typography.module.scss';

	button {
		margin: 0;
		padding: 0;
		border: none;
	}

	[class*='button-'] {
		@include label-large;
		cursor: pointer;
		overflow: hidden;
		position: relative;
		user-select: none;
		display: inline-flex;
		vertical-align: top;
		align-items: center;
		height: 40px;
		border-radius: 20px;
		padding: 0 24px;
		transition: all 0.2s var(--md-sys-motion-easing-standard);
	}

	.slot {
		display: flex;
		align-items: center;
		gap: 8px;
		box-sizing: border-box;
	}

	.icon-button {
		padding-left: 16px;
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

	@mixin defaultTint($color) {
		.tint {
			background-color: $color;
		}

		&:hover .tint {
			opacity: 0.08;
		}
		&:active .tint {
			opacity: 0.16;
		}
	}

	.button-elevated {
		background-color: var(--md-sys-color-surface);
		color: var(--md-sys-color-primary);
		box-shadow: var(--md-sys-elevation-level1);

		path {
			fill: var(--md-sys-color-primary);
		}
		.tint {
			background-color: var(--md-sys-color-primary);
			opacity: 0.08;
		}

		&:hover {
			box-shadow: var(--md-sys-elevation-level2);
			.tint {
				opacity: 0.16;
			}
		}

		&:active .tint {
			opacity: 0.2;
		}
	}

	.button-filled {
		background-color: var(--md-sys-color-primary);
		color: var(--md-sys-color-on-primary);
		@include defaultTint(var(--md-sys-color-on-primary));

		path {
			fill: var(--md-sys-color-on-primary);
		}

		&:hover {
			box-shadow: var(--md-sys-elevation-level1);
		}
	}

	.button-tonal {
		background-color: var(--md-sys-color-secondary-container);
		color: var(--md-sys-color-on-secondary-container);
		@include defaultTint(var(--md-sys-color-on-secondary-container));

		path {
			fill: var(--md-sys-color-on-secondary-container);
		}

		&:hover {
			box-shadow: var(--md-sys-elevation-level1);
		}
	}

	.button-outlined {
		background-color: transparent;
		color: var(--md-sys-color-primary);
		border: 1px solid var(--md-sys-color-outline);
		@include defaultTint(var(--md-sys-color-primary));

		path {
			fill: var(--md-sys-color-primary);
		}
	}

	.button-text {
		background-color: transparent;
		color: var(--md-sys-color-primary);
		padding: 0 12px;
		@include defaultTint(var(--md-sys-color-primary));

		path {
			fill: var(--md-sys-color-primary);
		}
	}
	.button-snackbar {
		background-color: transparent;
		color: var(--md-sys-color-inverse-primary);
		padding: 0 12px;
		@include defaultTint(var(--md-sys-color-primary));
	}
</style>
