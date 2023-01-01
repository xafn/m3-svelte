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
		padding: 0 1rem;
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
		gap: 1.5rem;
	}

	.bar-center {
		height: 4rem;

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
			padding-left: 1.5rem;
			padding-right: 1.5rem;
		}
	}

	.bar-small {
		height: 4rem;

		.title {
			align-items: flex-start;
			padding-left: 1rem;
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
			padding-top: 0.75rem;
			padding-bottom: 1.25rem;
			padding-left: 1rem;
			padding-right: 1rem;
			align-items: flex-start;

			// temp
			.nav-icon {
				margin-left: -0.5rem;
			}

			.trailing-icons {
				margin-left: auto;
			}
		}

		&medium {
			height: 7rem;
		}
		&large {
			height: 9.5rem;
		}
	}

	// @media screen and (max-width: 37.5rem) {
	//     .trailing-icons > :nth-child(1) {
	//         display: none;
	//     }
	// }
</style>
