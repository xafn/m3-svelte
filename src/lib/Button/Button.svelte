<script lang="ts">
	import Svg from '$lib/SVG/Svg.svelte';

	/**
	 * Specify the type of button. Snackbar type should not be used anywhere except snackbars.
	 * @type {"elevated" | "filled" | "tonal" | "outlined" | "text" | "snackbar"}
	 */
	export let type = 'filled';
	export let disabled = false;
	export let fullWidth = false;

	/**
	 * Pass in an SVG path.
	 */
	export let icon = '';

	let ripple = false;
	let timeout: ReturnType<typeof setTimeout>;
	function rippleAnimation() {
		ripple = false;
		timeout = setTimeout(() => (ripple = true), 1);
	}
</script>

<!-- 
  @component
  **Common buttons**  
  Buttons help people initiate actions, from sending an email, to sharing a document, to liking a 
  post. There are five types of common buttons: elevated, filled, filled tonal, outlined, and text.
  
  *** 
  **Example usage**   
   
  ```tsx
	<Button type="filled" on:click={makePayment}>Make payment</Button>
  ```
  ***
  [M3 guidelines](https://m3.material.io/components/buttons/guidelines)
 -->
<button
	on:click
	on:click={rippleAnimation}
	class="{icon ? 'icon-button' : ''} button-{type}"
	class:fullWidth
>
	{#if ripple}
		<span class="ripple" class:animation={ripple} />
	{/if}
	<span class="tint" />
	<div class="slot">
		{#if icon}
			<Svg viewBoxHeight={48} svgHeight={18}>
				<path d={icon} />
			</Svg>
		{/if}

		{#if $$slots}
			<slot />
		{/if}
	</div>
</button>

<style lang="scss">
	@import '../../styles/typography.module.scss';

	button {
		@include label-large;
		margin: 0;
		padding: 0;
		border: none;
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

	.ripple {
		position: absolute;
		margin-left: auto;
		margin-right: auto;
		opacity: 0;
		left: 0;
		right: 0;
		height: 100%;
		transition: all 0.2s var(--md-sys-motion-easing-standard);
		pointer-events: none;
		aspect-ratio: 1 / 1;
		margin: auto;
		border-radius: 100px;

		@keyframes ripple {
		to {
			transform: scale(8);
			opacity: 0;
		}
	}

		&.animation {
			opacity: 0.08;
			animation: ripple 1s forwards ease-out;
		}
	}


	.fullWidth {
		width: 100%;
		justify-content: center;
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
		.tint,
		.ripple {
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
		.tint,
		.ripple {
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
