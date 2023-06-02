<script lang="ts">
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	let Vehicles: any = [];

	function loadVehciles() {
		Vehicles = [];
		if (typeof window !== 'undefined') {
			for (let ID of Object.keys(localStorage)) {
				Vehicles = [...Vehicles, JSON.parse(localStorage.getItem(ID) as string)];
			}
			Vehicles.sort((a: any, b: any) => +a.ID - +b.ID);
		}
	}

	function removeVehciles(ID: string) {
		if (Vehicles.length == 1) {
			goto('/');
		} else {
			goto(`/${Vehicles[0].ID}`);
		}
		localStorage.removeItem(ID);
		Vehicles = Vehicles.filter((obj: any) => {
			return obj.ID !== ID;
		});
	}

	onMount(() => {
		loadVehciles();
	});
	$: $page.params.ID, loadVehciles();
</script>

<div class="container">
	<p>Seznam vozidel</p>
	{#each Vehicles as { ID, brand, model, year }}
		<div class="row">
			<p>
				<a href="/{ID}" style="color: {ID == $page.params.ID ? 'green' : 'black'};"
					>{brand} {model} {year}</a
				>
			</p>
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<svg
				on:click={() => {
					removeVehciles(ID);
				}}
				xmlns="http://www.w3.org/2000/svg"
				class="icon icon-tabler icon-tabler-trash-x"
				width="24"
				height="24"
				viewBox="0 0 24 24"
				stroke-width="2"
				stroke={ID == $page.params.ID ? 'green' : 'currentColor'}
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
	{/each}
</div>

<style>
	.container {
		width: 100%;
		max-width: 800px;
		padding-inline: 20px;
		background-color: #f2f2f2;
		border: 1px solid #ccc;
		border-radius: 5px;
	}
	.row {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	a {
		text-decoration: none;
		color: black;
	}
</style>
