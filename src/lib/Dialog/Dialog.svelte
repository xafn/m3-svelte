<script lang="ts">
	import { fade } from 'svelte/transition';
	import { quadInOut } from 'svelte/easing';
	import Svg from '$lib/SVG/Svg.svelte';
	export let open = false;
	export let fullscreen = false;
	/**
	 * Pass in an SVG path. Do not add an icon if there is no title.
	 */
	export let icon = '';
</script>

<!-- 
  @component
  **Dialogs**  
  Dialogs can require an action, communicate information, or help users 
  accomplish a task. There are two types of dialogs: basic and full-screen.
  
  *** 
  **Example usage**   
   
  ```tsx
  <Dialog>
	   <svelte:fragment slot="title">Hey there!</svelte:fragment>
	   <svelte:fragment slot="description">
			A dialog is a type of modal window that appears in front of app content 
			to provide critical information, or prompt for decision to be made.
		</svelte:fragment>
		<svelte:fragment slot="primaryButton">
			<Button on:click={() => open = !open}>
				Dismiss
			</Button>
		</svelte:fragment>
  </Dialog>
  ```
  ***
  [M3 guidelines](https://m3.material.io/components/dialogs/guidelines)
 -->
{#if open}
	<div
		class="modal"
		role="dialog"
		class:fullscreen
		aria-modal="true"
		transition:fade={{ easing: quadInOut, duration: 150 }}
	>
		<div class="main">
			<div class="header" class:icon>
				{#if icon}
					<Svg viewBoxHeight={48} svgHeight={24}>
						<path d={icon} />
					</Svg>
				{/if}
				{#if $$slots.title}
					<div class="title">
						<slot name="title" />
					</div>
				{/if}
			</div>

			{#if $$slots.description}
				<div class="description">
					<slot name="description" />
				</div>
			{/if}
		</div>

		<div class="buttons">
			{#if $$slots.buttonSecondary}
				<slot name="buttonSecondary" />
			{/if}
			{#if $$slots.buttonPrimary}
				<slot name="buttonPrimary" />
			{/if}
		</div>

		<div class="slot"><slot /></div>
	</div>
	<span class="scrim" on:click={() => (open = !open)} on:keypress={() => (open = !open)} />
{/if}

<style lang="scss">
	@import '../../styles/typography.module.scss';

	.modal {
		background-color: var(--md-sys-color-surface);
		min-width: 280px;
		max-width: 560px;
		position: fixed;
		overflow-y: scroll;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		border-radius: 28px;
		padding: 24px;
		z-index: 999;

		&::-webkit-scrollbar {
			display: none;
		}
	}

	.header {
		display: flex;
		justify-content: flex-start;
		gap: 16px;
	}

	.icon {
		flex-direction: column;
		align-items: center;

		path {
			fill: var(--md-sys-color-secondary);
		}
	}

	.title {
		@include headline-small;
		color: var(--md-sys-color-on-surface);
	}

	.description {
		@include body-medium;
		color: var(--md-sys-color-on-surface-variant);
		padding-top: 16px;
	}

	.buttons {
		padding-top: 24px;
		display: flex;
		gap: 8px;
		justify-content: flex-end;
	}

	.scrim {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.5);
		z-index: 998;
	}
</style>
