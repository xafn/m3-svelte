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
		width: 52px;
		height: 32px;

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
		border-radius: 100px;
		border: 2px solid var(--md-sys-color-outline);
		background-color: var(--md-sys-color-surface-variant);

		&:before {
			position: absolute;
			display: flex;
			align-items: center;
			justify-content: center;
			content: '';
			height: 16px;
			width: 16px;
			left: 6px;
			bottom: 6px;
			border-radius: 100px;
			background-color: var(--md-sys-color-outline);
			transition: all 0.4s var(--md-sys-motion-easing-standard);
		}

		&::after {
			position: absolute;
			opacity: 0;
			left: -10px;
			top: -10px;
			content: '';
			border-radius: 100px;
			height: 48px;
			width: 48px;
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
			transform: translateX(20px);
			height: 24px;
			width: 24px;
			left: 2px;
			bottom: 2px;
		}

		+ .slider::after {
			background-color: var(--md-sys-color-on-surface-variant);
			transform: translateX(20px);
		}
	}

	.switch:active .slider:before {
		transition-delay: 0.2s;
		height: 28px;
		width: 28px;
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
