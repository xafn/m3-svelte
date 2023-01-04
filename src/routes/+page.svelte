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
				Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum vestibulum urna ligula,
				a porta mi fermentum aliquam. Proin vulputate placerat consectetur. Curabitur dui neque,
				bibendum vel sodales ac, blandit non mi. Quisque ante odio, elementum vehicula magna id,
				volutpat congue ante. Nam pulvinar mauris id neque ornare, sed vulputate dui condimentum.
				Vestibulum sagittis pretium lacus a fermentum. Sed at arcu id velit tincidunt luctus in a
				enim. Aenean aliquam sagittis pharetra. Maecenas at blandit sem, vel congue velit. Nunc
				commodo consectetur venenatis. Cras ac vestibulum odio.
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
			<TextInput closeIcon />
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
			<Chip type="input">Suggestion</Chip>
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
					Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum vestibulum urna
					ligula, a porta mi fermentum aliquam. Proin vulputate placerat consectetur. Curabitur dui
					neque, bibendum vel sodales ac, blandit non mi. Quisque ante odio, elementum vehicula
					magna id, volutpat congue ante. Nam pulvinar mauris id neque ornare, sed vulputate dui
					condimentum. Vestibulum sagittis pretium lacus a fermentum. Sed at arcu id velit tincidunt
					luctus in a enim. Aenean aliquam sagittis pharetra. Maecenas at blandit sem, vel congue
					velit. Nunc commodo consectetur venenatis. Cras ac vestibulum odio. Integer non blandit
					magna, scelerisque tincidunt dolor. Phasellus hendrerit arcu at velit semper sagittis.
					<br/>
					Proin congue vestibulum metus vitae suscipit. Duis iaculis vestibulum metus, eget
					fermentum libero porta ut. Etiam vitae magna id ante blandit vestibulum id sed sem. Cras
					finibus nisl at lectus volutpat, vel tristique ex tempor. Sed euismod, justo ac tincidunt
					tempus, arcu odio lacinia diam, id imperdiet nisl ligula at purus. Praesent sagittis nisl
					in lorem ullamcorper mollis. Nunc sodales nisi fringilla ante hendrerit dignissim. Fusce
					scelerisque cursus justo, in tempus dui posuere ac. Mauris vitae diam tristique, ornare
					augue eu, gravida erat. In auctor eget purus et lobortis. Nam nec libero scelerisque mi
					porttitor gravida.
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
