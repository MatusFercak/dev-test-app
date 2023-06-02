<script lang="ts">
	import { goto } from '$app/navigation';

	let bindBrand: string | undefined;
	let bindModel: string | undefined;
	let bindYear: string | undefined;

	function addVehicle() {
		const carID: string = `${+new Date()}`;
		const carObject: { ID: string; brand: string; model: string; year: string } = {
			ID: carID,
			brand: bindBrand as string,
			model: bindModel as string,
			year: bindYear as string
		};
		bindBrand = undefined;
		bindModel = undefined;
		bindYear = undefined;
		localStorage.setItem(carID, JSON.stringify(carObject));
		goto(`/${carID}`);
	}
</script>

<div class="container">
	<div class="row">
		<label for="brand">Značka:</label>
		<input bind:value={bindBrand} type="text" id="brand" name="brand" />
	</div>

	<div class="row">
		<label for="model">Model:</label>
		<input bind:value={bindModel} type="text" id="model" name="model" />
	</div>

	<div class="button-row">
		<label for="year">Rok:</label>
		<input bind:value={bindYear} type="text" id="year" name="year" />
		<button
			on:click={() => {
				addVehicle();
			}}>Vložit</button
		>
	</div>
</div>

<style>
	.container {
		width: 100%;
		max-width: 800px;
		margin: 0 auto;
		margin-bottom: 10px;
		padding: 20px;
		background-color: #f2f2f2;
		border: 1px solid #ccc;
		border-radius: 5px;
	}
	input[type='text'] {
		width: 100%;
		padding: 8px;
		font-size: 16px;
		border: 1px solid #ccc;
		border-radius: 4px;
	}
	label {
		display: block;
		margin-top: 10px;
	}
	.row {
		margin: 0 auto;
		max-width: 800px;
		display: flex;
		align-items: center;
		margin-bottom: 10px;
	}

	.button-row {
		display: flex;
		justify-content: space-between;
		text-align: right;
		align-items: center;
	}

	.button-row button {
		padding: 8px 16px;
		font-size: 16px;
		border-radius: 4px;
	}
</style>
