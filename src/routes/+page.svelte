<script lang="ts" type="module">
	import VehicleDetails from '../lib/components/VehicleDetails.svelte';
	import VehicleForm from '../lib/components/VehicleForm.svelte';
	import VehicleList from '../lib/components/VehicleList.svelte';
</script>

<VehicleForm />
<div class="row">
	<div class="column">
		<VehicleList />
	</div>
	<div class="column">
		<VehicleDetails />
	</div>
</div>

<style>
	.row {
		max-width: 880px;
		margin: 0 auto;
		display: grid;
		padding: 0px;
		gap: 10px;
		grid-template-columns: 425px 425px;
	}
	.column {
		padding-inline: 20px;
		height: 250px;
	}
</style>
