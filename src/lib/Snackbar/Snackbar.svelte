<script lang="ts">
	import Button from '$lib/Button/Button.svelte';
	import { slide, fade } from 'svelte/transition';
	import { expoOut } from 'svelte/easing';
	export let open = false;

	let timeout: ReturnType<typeof setTimeout>;
	$: if (open) {
		clearTimeout(timeout);
		timeout = setTimeout(() => (open = false), 3000);
	}

</script>

{#if open}
	<div class="snackbar" 
    in:slide|local={{ duration: 400, easing: expoOut }}
    out:fade|local={{ duration: 300, easing: expoOut }}
    >
		<div class="text">
			<slot name="text" />
		</div>
		{#if $$slots.button}
			<div class="button">
				<Button type="snackbar"><slot name="button" /></Button>
			</div>
		{/if}
	</div>
{/if}

<style lang="scss">
	@import '../../styles/typography.module.scss';

	.snackbar {
		padding-top: 4px;
		padding-bottom: 4px;
		padding-left: 16px;
		padding-right: 8px;
		display: flex;
		justify-content: space-between;
		gap: 24px;
		align-items: center;
		border-radius: 4px;
		min-width: 200px;
		max-width: 560px;
		position: fixed;
		margin-left: 36px;
		margin-right: 36px;
		left: 0;
		right: 0;
		bottom: 2rem;
		background-color: var(--md-sys-color-inverse-surface);
		box-shadow: var(--md-sys-elevation-level3);
		transition: all 0.4s var(--md-sys-motion-easing-standard);
	}

	.text {
		@include body-medium;
		color: var(--md-sys-color-inverse-on-surface);
	}

	.button {
		align-items: flex-end;
	}
</style>
