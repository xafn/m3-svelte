<script>
	export let checked = false;
	export let disabled = false;
</script>

<label class="switch">
	<input type="checkbox" on:click bind:checked {disabled} />
	<span class="slider" />
</label>

<style lang="scss">
	.switch {
		position: relative;
		display: inline-block;
		width: 3.25rem;
		height: 2rem;

		input {
			opacity: 0;
			width: 0;
			height: 0;
		}
	}

	.slider {
		position: absolute;
		cursor: pointer;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		transition: 0.4s;
		border-radius: 6.25rem;
		border: 0.125rem solid var(--md-sys-color-outline);
		background-color: var(--md-sys-color-surface-variant);

		&:before {
			position: absolute;
			display: flex;
			align-items: center;
			justify-content: center;
			content: '';
			height: 1rem;
			width: 1rem;
			left: 0.375rem;
			bottom: 0.375rem;
			border-radius: 6.25rem;
			background-color: var(--md-sys-color-outline);
			transition: all 0.4s var(--md-sys-motion-easing-standard);
		}

		&::after {
			position: absolute;
			opacity: 0;
			left: -0.625rem;
			top: -0.625rem;
			content: '';
			border-radius: 6.25rem;
			height: 3rem;
			width: 3rem;
			background-color: var(--md-sys-color-on-surface);
			transition: all 0.4s var(--md-sys-motion-easing-standard);
		}

		&:hover::after {
			opacity: 0.08;
		}
	}

	input:checked {
		+ .slider {
			border-color: var(--md-sys-color-primary);
			background-color: var(--md-sys-color-primary);
		}

		+ .slider:before {
			background-color: var(--md-sys-color-on-primary);
			transform: translateX(1.25rem);
			height: 1.5rem;
			width: 1.5rem;
			left: 0.125rem;
			bottom: 0.125rem;
		}

		+ .slider::after {
			background-color: var(--md-sys-color-on-surface-variant);
			transform: translateX(1.25rem);
		}
	}

	.switch:active .slider:before {
		transition-delay: 0.2s;
		height: 1.75rem;
		width: 1.75rem;
		left: 0;
		bottom: 0;
	}

	.switch:hover {
		.slider:before {
			background-color: var(--md-sys-color-on-surface-variant);
		}

		input:checked + .slider:before {
			background-color: var(--md-sys-color-primary-container);
		}
	}
</style>
