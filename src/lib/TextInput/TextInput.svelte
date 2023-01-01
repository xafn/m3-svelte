<script lang="ts">
	export let placeholder = 'hiii';
	export let type = 'filled';
	let hasText: string;
</script>

<div class="text-input-container">
	<input class="input-{type}" type="text" class:hasText bind:value={hasText} />
	<span class="placeholder">{placeholder}</span>
	{#if type === 'filled'}
		<span class="bottom-line" />
	{/if}
</div>

<style lang="scss">
	@import '../../styles/typography.module.scss';

	.text-input-container {
		position: relative;
		display: inline-block;
		height: 3.5rem;
	}

	// impossible to animate default placeholder without a bunch of js
	input::placeholder {
		display: none;
		opacity: 0;
		visibility: hidden;
	}

	.placeholder {
		@include body-large;
		transition: all 0.2s var(--md-sys-motion-easing-standard);
		position: absolute;
		left: 1.125rem;
		top: 1.125rem;
		color: var(--md-sys-color-on-surface-variant);
		pointer-events: none;
		user-select: none;
	}

	input {
		@include body-large;
		height: 2.5rem;
		transition: all 0.3s var(--md-sys-motion-easing-standard);
		box-sizing: border-box;
		height: 3.5rem;
		vertical-align: top;
	}

	.input-filled {
		border-radius: 0.25rem 0.25rem 0 0;
		border: none;
		color: var(--md-sys-color-on-surface);
		background-color: var(--md-sys-color-surface-variant);
		border-bottom: 0.0625rem solid var(--md-sys-color-on-surface-variant);
		padding: 1rem 1rem 0 1rem;

		&:focus {
			outline: none;

			+ .placeholder {
				@include body-small;
				color: var(--md-sys-color-primary);
				transform: translateY(-0.625rem);
			}

			~ .bottom-line {
				width: 100%;
			}
		}
	}

	.bottom-line {
		height: 0.125rem;
		width: 0;
		margin-left: auto;
		margin-right: auto;
		right: 0;
		left: 0;
		bottom: 0;
		position: absolute;
		z-index: 1;
		background-color: var(--md-sys-color-primary);
		transition: all 0.3s var(--md-sys-motion-easing-standard);
	}

	.input-outlined {
		border-radius: 0.25rem;
		color: var(--md-sys-color-on-surface);
		background-color: transparent;
		border: 0.0625rem solid var(--md-sys-color-outline);
		padding: 0.5rem 1rem;

		+ .placeholder {
			padding: 0 0.25rem;
			background-color: var(--md-sys-color-background);
		}

		&:focus {
			outline: none;
			border-color: var(--md-sys-color-primary);

			+ .placeholder {
				@include body-small;
				color: var(--md-sys-color-primary);
				transform: translateY(-1.5rem);
			}
		}
	}

	.hasText {
		&.input-filled + .placeholder {
			@include body-small;
			transform: translateY(-0.625rem);
		}

		&.input-outlined + .placeholder {
			@include body-small;
			transform: translateY(-1.5rem);
		}
	}
</style>
