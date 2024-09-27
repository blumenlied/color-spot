<script>
	import Circle from './Circle.svelte'; // Ensure you import your Circle component

	let gridSize = 9; // Total number of circles
	let circles = []; // Array to hold the circle objects
	let hp = 5; // Initial HP
	let score = 0; // Initial score

	// Function to generate a random base color in RGB format
	function getRandomColor() {
		const r = Math.floor(Math.random() * 256);
		const g = Math.floor(Math.random() * 256);
		const b = Math.floor(Math.random() * 256);
		return `rgb(${r}, ${g}, ${b})`;
	}

	// Function to slightly alter a color (change RGB by a small amount)
	function getSlightlyDifferentColor(baseColor) {
		const colorValues = baseColor.match(/\d+/g).map(Number);
		const variation = colorValues.map((value) => {
			let newValue = value + Math.floor(Math.random() * 21) - 20; // ±10 variation
			return Math.max(0, Math.min(255, newValue)); // Clamp between 0 and 255
		});
		return `rgb(${variation[0]}, ${variation[1]}, ${variation[2]})`;
	}

	// Function to initialize the circles with random colors and one slightly different
	function initializeCircles() {
		circles = []; // Reset circles array
		const baseColor = getRandomColor(); // Generate a base color
		for (let i = 0; i < gridSize - 1; i++) {
			circles.push({
				color: baseColor,
				isSpecial: false // Mark all normal circles as not special
			});
		}
		// Add one special color that is slightly different from the base color
		const specialColor = getSlightlyDifferentColor(baseColor);
		circles.push({
			color: specialColor,
			isSpecial: true // Mark this circle as the special one
		});
		circles = shuffle(circles); // Shuffle after creating the array
	}

	// Function to shuffle the circles array
	function shuffle(array) {
		let currentIndex = array.length;
		while (currentIndex !== 0) {
			let randomIndex = Math.floor(Math.random() * currentIndex);
			currentIndex--;
			[array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
		}
		return array;
	}

	function resetGame() {
		score = 0;
		hp = 5;
		initializeCircles(); // Reinitialize circles
	}

	function handleCircleClick(circle) {
		// Check if the clicked circle is the special one
		if (circle.isSpecial) {
			score += 1; // Increment score
			initializeCircles(); // Reinitialize circles
		} else {
			hp -= 1; // Decrement HP
			if (hp <= 0) {
				alert('Game Over! Final Score: ' + score);
				resetGame();
			}
		}
	}

	initializeCircles(); // Initialize circles on component load
</script>

<div class="main">
	<h1>{hp} HP | {score} SCORE</h1>
	<div class="board">
		{#each circles as circle}
			<Circle color={circle.color} onClick={() => handleCircleClick(circle)} />
		{/each}
	</div>
</div>

<style>
	h1 {
		margin: 0;
		margin-bottom: 20px;
		color: #ff3e00;
		font-size: 4em;
		font-weight: 100;
	}

	.main {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 1em;
	}
	.board {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		width: 398px;
	}
</style>
