<script lang="ts">
	let heightCm: number;
	let weightKg: number;
	let resultBMI: number;
	let category: string;

	function buttonClick() {
		resultBMI = calculateBMI();
		category = categoryBMI();
	}

	function calculateBMI(): number {
		const heightMeters: number = heightCm / 100;
		const bmi: number = weightKg / (heightMeters * heightMeters);

		const roundedBmi = Math.round(bmi * 100) / 100;

		if (isNaN(roundedBmi) || !isFinite(roundedBmi) || weightKg == 0) {
			return NaN;
		}
		console.log(resultBMI);

		return roundedBmi;
	}

	function categoryBMI(): string {
		if (isNaN(resultBMI)) {
			return 'Enter valid height and weight!';
		} else if (resultBMI < 18.5) {
			return 'You are underweight. Eat more!';
		} else if (resultBMI >= 18.5 && resultBMI < 24.9) {
			return 'You are normal.';
		} else if (resultBMI >= 24.9 && resultBMI < 29.9) {
			return 'You are overweight. Eat less!';
		} else {
			return 'You are obese. Take care of your health!';
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

		<button on:click={buttonClick} type="button" class="btn variant-filled">Calculate BMI</button>

		{#if resultBMI && category}
			<p>Your Body Mass Index is: {resultBMI ? resultBMI : ''}, {category ? category : ''}</p>
		{:else if isNaN(resultBMI) || weightKg === 0}
			<p>{category ? category : ''}</p>
		{/if}
	</div>
</div>
