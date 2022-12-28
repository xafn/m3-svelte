<script lang="ts">
	export let placeholder = 'hiii';
	let hasText: string;
</script>

<div class="text-input-container">
	<input type="text" class:hasText bind:value={hasText} />
	<span class="placeholder">{placeholder}</span>
</div>

<style lang="scss">
	@import '../../styles/typography.module.scss';

	input {
		@include body-large;
		height: 40px;
		padding-top: 14px;
		padding-left: 16px;
		padding-right: 16px;
		border-radius: 4px 4px 0 0;
		border: none;
		color: var(--md-sys-color-on-surface);
		background-color: var(--md-sys-color-surface-variant);
		border-bottom: 1px solid var(--md-sys-color-on-surface-variant);
	}

	input::placeholder {
		display: none;
		opacity: 0;
		visibility: hidden;
	}

	.text-input-container {
		position: relative;
		display: inline-block;
		height: 56px;
	}

	.placeholder {
		@include body-large;
		color: var(--md-sys-color-on-surface-variant);
		transition: all 0.2s var(--md-sys-motion-easing-standard);
		background-color: var(--md-sys-color-surface-variant);
		position: absolute;
		left: 16px;
		top: 18px;
	}

	input:focus {
		opacity: 1;
		outline: none;
		border-bottom-color: var(--md-sys-color-primary);

		+ .placeholder {
			@include body-small;
			opacity: 1;
			visibility: visible;
			color: var(--md-sys-color-primary);
			transform: translateY(-10px);
		}
	}

	.hasText + .placeholder {
		@include body-small;
		transform: translateY(-10px);
	}
</style>
