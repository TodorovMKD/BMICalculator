<script lang="ts">
	let heightCm: number;
	let weightKg: number;
	let resultBMI: number;

	let category: any = categoryBMI();

	function calculateBMI() {
		const heightMeters: number = heightCm / 100;
		const bmi: number = weightKg / (heightMeters * heightMeters);

		resultBMI = bmi;

		categoryBMI();
	}

	function categoryBMI() {
		if (resultBMI < 18.5) {
			category = 'You are underweight. Eat more!';
		}
		if (resultBMI >= 18.51 && resultBMI < 24.9) {
			category = 'You are normal.';
		}
		if (resultBMI >= 24.91 && resultBMI < 29.9) {
			category = 'You are overweight. Eat less!';
		}
		if (resultBMI >= 29.91) {
			category = 'You are overweight. Eat less!';
		}
	}
</script>

<div class="static container h-full mx-auto flex justify-center items-center">
	<div class="space-y-5">
		<label class="label">
			<span>Weight:</span>
			<input bind:value={weightKg} class="input" type="text" placeholder="Weight in kg..." />
		</label>
		<label class="label">
			<span>Height:</span>
			<input bind:value={heightCm} class="input" type="text" placeholder="Height in cm..." />
		</label>

		<button on:click={calculateBMI} type="button" class="btn variant-filled">Calculate BMI</button>

		{#if resultBMI && category}
			<p>Your Body Mass Index is: {resultBMI ? resultBMI : ''}, {category ? category : ''}</p>
		{/if}
	</div>
</div>
