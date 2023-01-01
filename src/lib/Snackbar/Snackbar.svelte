<script lang="ts">
	import { slide, fade } from 'svelte/transition';
	import { expoOut } from 'svelte/easing';
	
	import Button from '$lib/Button/Button.svelte';
	import Svg from '$lib/SVG/Svg.svelte';
	export let open = false;
	export let closeIcon = false;
	export let dismissTime = 3000;

	let timeout: ReturnType<typeof setTimeout>;
	$: if (open) {
		clearTimeout(timeout);
		timeout = setTimeout(() => (open = false), dismissTime);
	}
</script>


{#if open}
	<div
		class="snackbar"
        class:closeIcon
		in:slide|local={{ duration: 400, easing: expoOut }}
		out:fade|local={{ duration: 300, easing: expoOut }}
	>
		<div class="text">
			<slot name="text" />
		</div>
		<div class="buttons">
		    {#if $$slots.button}
    			<div class="button">
    				<Button type="snackbar"><slot name="button" /></Button>
    			</div>
    		{/if}
    		{#if closeIcon}
    			<button on:click={() => open = !open}>
    			    <Svg viewBoxHeight={48} svgHeight={24}>
        				<path
        					d="m12.45 38.35-2.8-2.8L21.2 24 9.65 12.45l2.8-2.8L24 21.2 35.55 9.65l2.8 2.8L26.8 24l11.55 11.55-2.8 2.8L24 26.8Z"
        				/>
        			</Svg>
    			</button >
    		{/if}
		</div>
	</div>
{/if}

<style lang="scss">
	@import '../../styles/typography.module.scss';

	.snackbar {
        display: flex;
		box-sizing: border-box;
		justify-content: space-between;
		padding-top: 0.25rem;
		padding-bottom: 0.25rem;
		padding-left: 1rem;
		padding-right: 0.5rem;
        height: 3rem;
		gap: 1.5rem;
		align-items: center;
		border-radius: 0.25rem;
		min-width: 12.5rem;
		max-width: 35rem;
		position: fixed;
		margin-left: 2.25rem;
		margin-right: 2.25rem;
		z-index: 99;
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

    button {
        background-color: transparent;
        padding: 0;
        margin: 0;
        border: none;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .buttons {
        display: flex;
        gap: 0.75rem;
        align-items: center;
    }

    .closeIcon {
        padding-right: 0.75rem;
		fill: var(--md-sys-color-inverse-on-surface);
    }

    .button {
		align-items: flex-end;
	}

</style>
