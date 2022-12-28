<script lang="ts">
	import { fade } from 'svelte/transition';
	import { quadInOut } from 'svelte/easing';
	import Button from '$lib/Button/Button.svelte';
	export let open = false;
	export let fullscreen = false;
	export let icon = '';
</script>

{#if open}
	<div
		class="modal"
		role="dialog"
		class:fullscreen
		aria-modal="true"
		transition:fade={{ easing: quadInOut, duration: 150 }}
	>
		<div class="main">
			<div class="headline-small title">
				{#if $$slots.title}
					<div class="title headline-small">
						<slot name="title" />
					</div>
				{/if}
			</div>

			{#if $$slots.description}
				<div class="description body-medium">
					<slot name="description" />
				</div>
			{/if}
		</div>

		<div class="buttons">
			{#if $$slots.buttonSecondary}
				<div on:click>
				    <Button type="text" on:click>
    					<slot name="buttonSecondary" />
    				</Button>
				</div>
			{/if}
			{#if $$slots.buttonPrimary}
				<div on:click>
				    <Button type="text" on:click>
    					<slot name="buttonPrimary" />
    				</Button>
				</div>
			{/if}
		</div>

		<div class="slot"><slot /></div>
	</div>
	<span class="scrim" on:click={() => (open = !open)}/>
{/if}

<style lang="scss">
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
	.title {
		color: var(--md-sys-color-on-surface);
		display: flex;
		justify-content: flex-start;
	}

	.description {
		padding-top: 16px;
		color: var(--md-sys-color-on-surface-variant);
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
