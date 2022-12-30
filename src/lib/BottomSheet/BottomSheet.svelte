<script lang="ts">
	import { fly, fade } from 'svelte/transition';
	import { expoOut } from 'svelte/easing';

	export let open = false;
	export let dragHandle = true;

	let drag = false;
	let noUserSelect = true;
	let top = 0;
	let timeout;
	let clientHeight;

	$: if (!open) {
		top = 0;
	}

	$: if (clientHeight < 100) {
		open = false;
	}

	function onMouseDown() {
		drag = true;
		noUserSelect = true;
	}

	function onMouseUp() {
		drag = false;
		clearTimeout(timeout);
		timeout = setTimeout(() => (noUserSelect = false), 1000);
	}

	function onMouseMove(e) {
		if (drag) {
			top -= e.movementY;
		}
	}
</script>

<svelte:window on:mouseup={onMouseUp} on:mousemove={onMouseMove} />

{#if open}
	<div
		class="bottom-sheet"
		bind:clientHeight
		style="height: fit-content; {top ? 'max-height: 100%;' : ''}"
		style:height="{clientHeight + top}px"
		transition:fly|local={{ y: 100, duration: 300, easing: expoOut }}
	>
		{#if dragHandle}
			<div class="drag-handle-touch-target" on:mousedown={onMouseDown}>
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
		max-width: 640px;
		max-height: 50%;
		margin-top: 72px;
		position: fixed;
		display: flex;
		align-items: center;
		flex-direction: column;
		overflow-y: scroll;
		transform: translate(-50%, 0%);
		left: 50%;
		bottom: 0;
		border-radius: 28px 28px 0 0;
		z-index: 999;
		box-shadow: var(--md-sys-elevation-level1);

		// temporary
		user-select: none;

		&::-webkit-scrollbar {
			display: none;
		}
	}
	.drag-handle {
		background-color: var(--md-sys-color-on-surface-variant);
		border-radius: 100px;
		height: 4px;
		width: 32px;
		opacity: 0.4;
	}

	.noUserSelect {
		user-select: none;
	}

	.drag-handle-touch-target {
		cursor: pointer;
		width: 25%;
		padding-top: 22px;
		padding-bottom: 22px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.slot {
		width: calc(100% - 48px);
		padding-bottom: 22px;
		padding-left: 24px;
		padding-right: 24px;
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
