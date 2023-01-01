<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade } from 'svelte/transition';
	import { draggable } from '@neodrag/svelte';

	import { expoOut } from 'svelte/easing';

	export let open = false;
	export let dragHandle = true;

	let noUserSelect = true;
	let sheetTop = 0;
	let sheetHeight: number;
	let initalClientHeight: number;
	let screenHeight: number
	let sheet: HTMLElement;


	onMount(() => {
		initalClientHeight = sheetHeight;
	});


	let maxheight = false;


	function dragger(e) {
		sheetTop = e.detail.domRect.y;
		screenHeight = e.path[5].clientHeight;
	}

	function dragStart() {
		maxheight = true;
	}

	$: if (!open) {
		maxheight = false;
	}

	// $: if (screenHeight - sheetTop < screenHeight / 2.5) {
	// 	open = false;
	// }
</script>

{#if open}
	<div
		class="bottom-sheet"
		class:maxheight
		bind:this={sheet}
		bind:clientHeight={sheetHeight}
		use:draggable={{
			handle: '.drag-handle-touch-target',
			axis: 'y',
			bounds: { top: 0, bottom: -initalClientHeight * 2 }
		}}
		on:neodrag={dragger}
		on:neodrag:start={dragStart}
		transition:fly|local={{ y: 100, duration: 300, easing: expoOut }}
	>
		{#if dragHandle}
			<div class="drag-handle-touch-target">
				<div class="drag-handle" />
			</div>
		{/if}
		<div class="slot" class:noUserSelect><slot /></div>
	</div>
	<span
		class="scrim"
		on:click={() => (open = !open)}
		on:keypress={() => (open = !open)}
		transition:fade|local={{ duration: 300, easing: expoOut }}
	/>
{/if}

<style lang="scss">
	@import '../../styles/typography.module.scss';

	.bottom-sheet {
		display: block;
		background-color: var(--md-sys-color-surface);
		width: 100%;
		max-width: 40rem;
		max-height: 50%;
		margin-right: auto;
		margin-left: auto;
		position: fixed;
		display: flex;
		align-items: center;
		flex-direction: column;
		overflow-y: scroll;
		left: 50%;
		top: 50%;
		height: 100vh;
		bottom: 0;
		border-radius: 1.75rem 1.75rem 0 0;
		z-index: 999;
		box-shadow: var(--md-sys-elevation-level1);
		transition: all 0.4s var(--md-sys-motion-easing-standard);

		// temporary
		user-select: none;

		&::-webkit-scrollbar {
			display: none;
		}
	}
	.drag-handle {
		background-color: var(--md-sys-color-on-surface-variant);
		border-radius: 6.25rem;
		height: 0.25rem;
		width: 2rem;
		opacity: 0.4;
	}

	.maxheight {
		max-height: 100%;
	}

	.drag-handle-touch-target {
		cursor: pointer;
		width: 25%;
		padding-top: 1.375rem;
		padding-bottom: 1.375rem;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.slot {
		width: calc(100% - 3rem);
		padding-bottom: 1.375rem;
		padding-left: 1.5rem;
		padding-right: 1.5rem;
		overflow-x: hidden;
		overflow-y: hidden;

		&::-webkit-scrollbar {
			display: none;
		}
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
