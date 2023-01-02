<script lang="ts">
	export let type = 'assist';
	export let icon = '';
	export let trailingIcon = '';
	export let elevated = false;
	export let open = true;
	let selected = false;
</script>

{#if open || type !== 'input'}
	<button
		on:click
		on:click={() => (selected = !selected)}
		class:selected
		class:elevated
		class:hasIcon={icon}
		class:hasTrailingIcon={trailingIcon}
		class="chip-{type}"
	>
		{#if icon}
			<div class="icon">{icon}</div>
		{/if}
		<slot />
		{#if trailingIcon === 'close'}
			<button on:click={() => (open = false)} class="icon">
				<div class="icon">{trailingIcon}</div>
			</button>
		{:else if trailingIcon}
			<div class="icon">{trailingIcon}</div>
		{/if}
	</button>
{/if}

<style lang="scss">
	@import '../../styles/typography.module.scss';

	button {
		display: inline-flex;
		margin: 0;
		padding: 0;
		border: none;
		background-color: transparent;
		cursor: pointer;
	}

	[class*='chip-'] {
		@include label-large;
		padding: 0 16px;
		height: 32px;
		border-radius: 8px;
		color: var(--md-sys-color-on-surface);
		border: 1px solid var(--md-sys-color-outline);
		position: relative;
		text-align: center;
		align-items: center;
		vertical-align: top;
		gap: 8px;
		transition: background-color 0.2s var(--md-sys-motion-easing-standard);
	}

	.icon {
		@include icon;
		font-size: 18px;
		color: var(--md-sys-color-primary);
	}

	.selected {
		background-color: var(--md-sys-color-secondary-container);
		color: var(--md-sys-color-on-surface);
	}

	.hasIcon {
		padding-left: 8px;
	}

	.hasTrailingIcon {
		padding-right: 8px;
	}
</style>
