<script lang="ts">
	export let type = 'elevated';

	// opininated padding but less work if you don't care
	export let defaultPadding = false;
</script>

<div class="card-{type}" class:defaultPadding>
	<div class="slot"><slot /></div>
	<span class="tint" />
</div>

<style lang="scss">
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

	[class*='card-'] {
		height: max-content;
		width: max-content;
		position: relative;
		border-radius: 12px;
		overflow: hidden;
	}

	.defaultPadding {
		padding: 16px;
	}

	.slot {
		text-align: start;
	}

	@mixin defaultTint($color, $hover: 0.08, $active: 0.16) {
		.tint {
			background-color: $color;
		}

		&:hover .tint {
			opacity: $hover;
		}
		&:active .tint {
			opacity: $active;
		}
	}

	.card-elevated,
	.card-outlined {
		background-color: var(--md-sys-color-surface);
		box-shadow: var(--md-sys-elevation-level1);
		@include defaultTint(var(--md-sys-color-on-surface), 0.16, 0.2);

		.tint {
			opacity: 0.08;
		}
	}

	.card-outlined {
		border: 1px solid var(--md-sys-color-outline);
	}

	.card-filled {
		background-color: var(--md-sys-color-surface-variant);
		@include defaultTint(var(--md-sys-color-on-surface-variant));
	}
</style>
