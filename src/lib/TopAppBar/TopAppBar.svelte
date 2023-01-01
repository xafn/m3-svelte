<script lang="ts">
	export let type = 'large';
	export let fixed = false;
	let y: number;
</script>

<svelte:window bind:scrollY={y} />

<header class="bar-{type}" class:fixed class:scrolled={fixed && y > 26}>
	<div class="top">
		{#if fixed}
			<span class="tint" />
		{/if}
		<div class="nav-icon">
			<slot name="nav-icon" />
		</div>
		{#if type === 'center' || type === 'small'}
			<div class="title">
				<slot name="title" />
			</div>
		{/if}
		<div class="trailing-icons">
			<slot name="trailing-icons" />
		</div>
	</div>
	{#if type === 'medium' || type === 'large'}
		<div class="title">
			<slot name="title" />
		</div>
	{/if}
</header>

<style lang="scss">
	@import '../../styles/typography.module.scss';

	header {
		box-sizing: border-box;
		padding: 0 16px;
		width: 100%;
		top: 0;
		left: 0;
		display: flex;
		align-items: center;
		transition: all 0.2s var(--md-sys-motion-easing-standard);
		background-color: var(--md-sys-color-surface);
		z-index: 100;
		position: relative;

		.top {
			box-sizing: border-box;
			width: 100%;
			display: flex;
			align-items: center;
		}
	}

	.fixed {
		position: fixed;
	}

	.tint {
		position: absolute;
		display: inline-block;
		pointer-events: none;
		z-index: 101;
		height: 100%;
		width: 100%;
		top: 0;
		left: 0;
		opacity: 0;
		transition: all 0.2s var(--md-sys-motion-easing-standard);
		background-color: var(--md-sys-color-on-surface);
	}

	.scrolled {
		box-shadow: var(--md-sys-elevation-level2);

		.tint {
			opacity: 0.08;
		}
	}

	.title {
		@include title-large;
		color: var(--md-sys-color-on-surface);
        width: max-content;
	}

	.trailing-icons {
		display: flex;
		gap: 24px;
	}

	.bar-center {
		height: 64px;

		.top {
			justify-content: space-between;
		}

		.title {
			position: absolute;
			margin-left: auto;
			margin-right: auto;
			left: 0;
			right: 0;
			text-align: center;
			padding-left: 24px;
			padding-right: 24px;
		}
	}

	.bar-small {
		height: 64px;

		.title {
			align-items: flex-start;
			padding-left: 16px;
		}

		.trailing-icons {
			margin-left: auto;
		}
	}

	.bar- {
		&medium,
		&large {
			flex-direction: column;
			justify-content: space-between;
			// temp padding top (need to do icon buttons)
			padding-top: 12px;
			padding-bottom: 20px;
			padding-left: 16px;
			padding-right: 16px;
			align-items: flex-start;

			// temp
			.nav-icon {
				margin-left: -8px;
			}

			.trailing-icons {
				margin-left: auto;
			}
		}

		&medium {
			height: 112px;
		}
		&large {
			height: 152px;
		}
	}

	// @media screen and (max-width: 600px) {
	//     .trailing-icons > :nth-child(1) {
	//         display: none;
	//     }
	// }
</style>
