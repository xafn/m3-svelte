<script>
	import Button from '$lib/Button/Button.svelte';
	import Dialogue from '$lib/Dialogue/Dialogue.svelte';
	import Divider from '$lib/Divider/Divider.svelte';
	import ProgressIndicator from '$lib/ProgressIndicator/ProgressIndicator.svelte';
	import Switch from '$lib/Switch/Switch.svelte';
	let modalOpen = false;
</script>

<ProgressIndicator />
<main class="wrapper">
	<h1>Material 3 Svelte</h1>
	<p>Svelte UI component library for Google's Material 3.</p>

	<div class="components">
		<div>
			<div class="label-large">Switch</div>
			<Switch />
		</div>

		<div>
			<div class="label-large">Progress Indicator</div>
			<ProgressIndicator value={29} />
		</div>

		<div>
			<div class="label-large">Buttons</div>
			<Button type="elevated">Elevated</Button>
			<Button type="filled">Filled</Button>
			<Button type="tonal">Tonal</Button>
			<Button type="outlined">Outlined</Button>
			<Button type="text">Text</Button>
		</div>

		<div>
			<div class="label-large">Divider</div>
			<Divider />
		</div>

		<div>
			<div class="label-large">Dialogue</div>
			<Button on:click={() => (modalOpen = !modalOpen)} type="tonal">Open Dialogue</Button>
		</div>
	</div>
	<Dialogue bind:open={modalOpen}>
		<svelte:fragment slot="title">This is a dialogue</svelte:fragment>
		<svelte:fragment slot="description">
			Dear reader, hope you have a wonderful day. And your tomorrow will be even better. First I
			have to make an excuse for my bad writing skills. I hope you are fine with some mistakes as
			english is not my main language. I only had it for some years at school. Second reason is this
			is very hard for me. I never told it to anyone. But I feel like you are ready for the real
			thing. Again, sorry for the bad english. Now to my big unfake. I'm actually 100% a girl.
			thought do it a little earlier than you predicted. Sorry also for this. Have a nice day. Best,
			the creatures under your skin
		</svelte:fragment>
		<svelte:fragment slot="buttonSecondary">Close</svelte:fragment>
		<svelte:fragment slot="buttonPrimary">Hi</svelte:fragment>
	</Dialogue>
</main>

<style>
	[class*='label-'] {
		margin-bottom: 0.5rem;
	}

	.components {
		display: flex;
		flex-direction: column;
		gap: 2rem;
	}
</style>
