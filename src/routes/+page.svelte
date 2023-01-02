<script lang="ts">
	import BottomSheet from '$lib/BottomSheet/BottomSheet.svelte';
	import Button from '$lib/Button/Button.svelte';
	import Card from '$lib/Card/Card.svelte';
	import Chip from '$lib/Chip/Chip.svelte';
	import Dialog from '$lib/Dialog/Dialog.svelte';
	import Divider from '$lib/Divider/Divider.svelte';
	import Fab from '$lib/FAB/FAB.svelte';
	// import Menu from '$lib/Menu/Menu.svelte';
	import ProgressIndicator from '$lib/ProgressIndicator/ProgressIndicator.svelte';
	import Snackbar from '$lib/Snackbar/Snackbar.svelte';
	import Switch from '$lib/Switch/Switch.svelte';
	import TextInput from '$lib/TextInput/TextInput.svelte';
	import TopAppBar from '$lib/TopAppBar/TopAppBar.svelte';
	let modalOpen = false;
	let snackbarOpen = false;
	let bottomSheetOpen = false;
	let inputChip = true;

	const appBars: { [key: string]: number } = {
		center: 6,
		small: 6,
		medium: 10,
		large: 12
	};

	let appBar = 'center';
	let index = 0;

	function appBarCycle() {
		index = index === 3 ? 0 : (index += 1);
		appBar = Object.keys(appBars)[index];
	}
</script>

<TopAppBar fixed type={appBar}>
	<svelte:fragment slot="nav-icon">
		<Button type="text" on:click={appBarCycle} icon="change_circle" />
	</svelte:fragment>
	<svelte:fragment slot="title">Svelte Material 3</svelte:fragment>
</TopAppBar>

<main class="wrapper" style="margin-top: {appBars[appBar]}rem">
	<h1>Svelte Material 3</h1>
	<p>Svelte UI component library for Google's Material 3.</p>

	<div class="components">
		<div>
			<div class="label-large">Switch</div>
			<Switch />
		</div>

		<div>
			<div class="label-large">Progress Indicator</div>
			<ProgressIndicator value={29} />
			<br />
			<ProgressIndicator />
		</div>

		<div>
			<div class="label-large">Buttons</div>
			<Button type="elevated">Elevated</Button>
			<Button type="filled" icon="camera">Filled</Button>

			<Button type="tonal" icon="edit">Tonal</Button>
			<Button type="outlined">Outlined</Button>
			<Button type="text">Text</Button>

			<div class="fabs">
				<Fab type="small" icon="web" />
				<Fab type="default" icon="support" />
				<Fab type="large" icon="edit" />
				<Fab type="extended" icon="extension">Extended??</Fab>
			</div>
		</div>

		<div>
			<div class="label-large">Divider</div>
			<Divider />
		</div>

		<div>
			<div class="label-large">Dialogue</div>
			<Button on:click={() => (modalOpen = !modalOpen)} type="tonal">Open Dialogue</Button>
		</div>

		<Dialog bind:open={modalOpen} icon="settings">
			<svelte:fragment slot="title">This is a dialogue</svelte:fragment>
			<svelte:fragment slot="description">
				Dear reader, hope you have a wonderful day. And your tomorrow will be even better. First I
				have to make an excuse for my bad writing skills. I hope you are fine with some mistakes as
				english is not my main language. I only had it for some years at school. Second reason is
				this is very hard for me. I never told it to anyone. But I feel like you are ready for the
				real thing. Again, sorry for the bad english. Now to my big unfake. I'm actually 100% a
				girl. thought do it a little earlier than you predicted. Sorry also for this. Have a nice
				day. Best, the creatures under your skin.
			</svelte:fragment>
			<svelte:fragment slot="buttonPrimary">
				<Button type="text" on:click={() => (modalOpen = !modalOpen)}>OK</Button>
			</svelte:fragment>
		</Dialog>

		<div>
			<div class="label-large">Snackbar</div>
			<Button on:click={() => (snackbarOpen = !snackbarOpen)} type="tonal">yum</Button>
		</div>

		<Snackbar bind:open={snackbarOpen} closeIcon>
			<svelte:fragment slot="text">This is a snackbar yum yum</svelte:fragment>
			<svelte:fragment slot="button">hey</svelte:fragment>
		</Snackbar>

		<div>
			<div class="label-large">Text Input</div>
			<TextInput />
			<TextInput type="outlined" />
		</div>

		<div>
			<div class="label-large">Bottom Sheet</div>
			<Button on:click={() => (bottomSheetOpen = !bottomSheetOpen)} type="outlined"
				>heh bottom</Button
			>
		</div>

		<!-- <div>
			<Menu />
		</div> -->

		<div>
			<div class="label-large">Chips</div>
			<Chip type="assist" icon="directions_car">Assist</Chip>
			<Chip type="filter" on:click={() => (inputChip = !inputChip)} icon="check">Filter</Chip>
			<Chip type="input" bind:open={inputChip} icon="settings" trailingIcon="close">Input</Chip>
			<Chip type="input" icon="logout">Suggestion</Chip>
		</div>
		<div>
			<div class="label-large">Card</div>
			<div class="cards">
				<Card type="elevated" defaultPadding>
					<div class="title-large">yoppers</div>
					<p>oh the misery iudfviufdhiuvdfiuhiu</p>

					<Button type="tonal">yop</Button>
				</Card>
				<Card type="filled" defaultPadding>
					<div class="title-large">yoppers</div>
					<p>oh the misery iudfviufdhiuvdfiuhiu</p>

					<Button type="outlined">yop</Button>
				</Card>
				<Card type="outlined" defaultPadding>
					<div class="title-large">yoppers</div>
					<p>oh the misery iudfviufdhiuvdfiuhiu</p>

					<Button type="filled">yop</Button>
				</Card>
			</div>
		</div>

		<BottomSheet bind:open={bottomSheetOpen}>
			<div class="bottom-sheet">
				<div class="title-large">Bottom Sheet</div>
				<p>oh the misery</p>
				<br />
				<Button fullWidth type="elevated">yoppers</Button>
				<p>
					What the fuck did you just fucking say about me, you little bitch? I'll have you know I
					graduated top of my class in the Navy Seals, and I've been involved in numerous secret
					raids on Al-Quaeda, and I have over 300 confirmed kills. I am trained in gorilla warfare
					and I'm the top sniper in the entire US armed forces. You are nothing to me but just
					another target. I will wipe you the fuck out with precision the likes of which has never
					been seen before on this Earth, mark my fucking words. You think you can get away with
					saying that shit to me over the Internet? Think again, fucker. As we speak I am contacting
					my secret network of spies across the USA and your IP is being traced right now so you
					better prepare for the storm, maggot. The storm that wipes out the pathetic little thing
					you call your life. You're fucking dead, kid. I can be anywhere, anytime, and I can kill
					you in over seven hundred ways, and that's just with my bare hands. Not only am I
					extensively trained in unarmed combat, but I have access to the entire arsenal of the
					United States Marine Corps and I will use it to its full extent to wipe your miserable ass
					off the face of the continent, you little shit. If only you could have known what unholy
					retribution your little "clever" comment was about to bring down upon you, maybe you would
					have held your fucking tongue. But you couldn't, you didn't, and now you're paying the
					price, you goddamn idiot. I will shit fury all over you and you will drown in it. You're
					fucking dead, kiddo.
				</p>
			</div>
		</BottomSheet>
	</div>
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

	.fabs,
	.cards {
		display: flex;
		flex-wrap: wrap;
		margin-top: 1rem;
		gap: 1rem;
	}
</style>
