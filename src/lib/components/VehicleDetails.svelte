<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	let Vehicle: any = {
		ID: undefined,
		brand: undefined,
		model: undefined,
		year: undefined
	};

	function loadVehicle() {
		if (typeof window !== 'undefined') {
			if ($page.params.ID !== undefined) {
				const VEHICLE = JSON.parse(localStorage.getItem($page.params.ID) as string);
				if (VEHICLE !== undefined && VEHICLE !== null) {
					Vehicle.ID = VEHICLE.ID;
					Vehicle.brand = VEHICLE.brand;
					Vehicle.model = VEHICLE.model;
					Vehicle.year = VEHICLE.year;
				} else {
					goto('/');
				}
			}
		}
	}

	function removeVehciles(ID: string) {
		goto('/');
		localStorage.removeItem(ID);
	}

	onMount(() => {
		loadVehicle();
	});

	$: $page.params.ID, loadVehicle();
</script>

<div class="container">
	<p>Detail vozidla</p>
	{#if Vehicle.ID}
		<div class="row">
			<p>
				{Vehicle.brand ? Vehicle.brand : ''}
				{Vehicle.model ? Vehicle.model : ''}
				{Vehicle.year ? Vehicle.year : ''}
			</p>
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<svg
				on:click={() => {
					removeVehciles(Vehicle.ID);
				}}
				xmlns="http://www.w3.org/2000/svg"
				class="icon icon-tabler icon-tabler-trash-x"
				width="24"
				height="24"
				viewBox="0 0 24 24"
				stroke-width="2"
				stroke="currentColor"
				fill="none"
				stroke-linecap="round"
				stroke-linejoin="round"
			>
				<path stroke="none" d="M0 0h24v24H0z" fill="none" />
				<path d="M4 7h16" />
				<path d="M5 7l1 12a2 2 0 0 0 2 2h8a2 2 0 0 0 2 -2l1 -12" />
				<path d="M9 7v-3a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v3" />
				<path d="M10 12l4 4m0 -4l-4 4" />
			</svg>
		</div>
	{/if}
</div>

<style>
	.container {
		width: 100%;
		max-width: 800px;
		padding-inline-start: 20px;
		background-color: #f2f2f2;
		border: 1px solid #ccc;
		border-radius: 5px;
	}
	.row {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
</style>
