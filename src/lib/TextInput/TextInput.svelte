<script lang="ts">
	export let placeholder = 'hiii';
	export let type = 'filled';
	let hasText: string;
</script>

<div class="text-input-container">
	<input class="input-{type}" type="text" class:hasText bind:value={hasText} />
	<span class="placeholder">{placeholder}</span>
</div>

<style lang="scss">
	@import '../../styles/typography.module.scss';

	.text-input-container {
		position: relative;
		display: inline-block;
		height: 56px;
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
		left: 18px;
		top: 18px;
		color: var(--md-sys-color-on-surface-variant);
		pointer-events: none;
		user-select: none;
	}

	input {
		@include body-large;
		height: 40px;
		transition: all 0.2s var(--md-sys-motion-easing-standard);
		box-sizing: border-box;
		height: 56px;
		vertical-align: top;
	}

	.input-filled {
		border-radius: 4px 4px 0 0;
		border: none;
		color: var(--md-sys-color-on-surface);
		background-color: var(--md-sys-color-surface-variant);
		border-bottom: 1px solid var(--md-sys-color-on-surface-variant);
		padding: 16px 16px 2px 16px;

		&:focus {
			outline: none;
			padding: 16px 16px 1px 16px;
			border-bottom: 2px solid var(--md-sys-color-primary);

			+ .placeholder {
				@include body-small;
				color: var(--md-sys-color-primary);
				transform: translateY(-10px);
			}
		}
	}

	.input-outlined {
		border-radius: 4px;
		color: var(--md-sys-color-on-surface);
		background-color: transparent;
		border: 1px solid var(--md-sys-color-outline);
		padding: 8px 16px;

		+ .placeholder {
			padding: 0 4px;
			background-color: var(--md-sys-color-background);
		}

		&:focus {
			outline: none;
			border-color: var(--md-sys-color-primary);

			+ .placeholder {
				@include body-small;
				color: var(--md-sys-color-primary);
				transform: translateY(-24px);
			}
		}
	}

	.hasText {
		&.input-filled + .placeholder {
			@include body-small;
			transform: translateY(-10px);
		}

		&.input-outlined + .placeholder {
			@include body-small;
			transform: translateY(-24px);
		}
	}
</style>
