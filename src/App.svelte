<script>
	import svelteLogo from './assets/svelte.svg';
	import viteLogo from '/vite.svg';
	import Counter from './lib/Counter.svelte';
	import { Loader } from '@googlemaps/js-api-loader';
	import { onMount } from 'svelte';
	
	const loader = new Loader({
		apiKey: '<<YOUR_API_KEY>>',
		version: 'weekly'
	});

	let map;
	let mapContainer;

	onMount(async () => {
		const { Map } = await loader.importLibrary('maps');
		map = new Map(mapContainer, {
			center: { lat: -34.397, lng: 150.644 },
			zoom: 8
		});
	});
</script>

<main>
	<div>
		<a href="https://vitejs.dev" target="_blank" rel="noreferrer">
			<img src={viteLogo} class="logo" alt="Vite Logo" />
		</a>
		<a href="https://svelte.dev" target="_blank" rel="noreferrer">
			<img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
		</a>
	</div>
	<h1>Vite + Svelte</h1>

	<div class="card">
		<Counter />
	</div>

	<div class="full-screen" bind:this={mapContainer}></div>
</main>

<style>
	.full-screen {
		width: 50vw;
		height: 90vh;
	}
</style>
