<script>
	export let color;
	export let onClick;

	function handleClick() {
		if (onClick) {
			onClick();
		}
	}
</script>

<button class="circle" on:click={handleClick} style="background-color: {color};"></button>

<style>
	.circle {
		width: 100px;
		height: 100px;
		border-radius: 50%; /* Makes the button circular */
		margin: 5px;
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer; /* Change cursor to pointer for clickable */
		outline: none; /* Removes the default outline */
		border: none; /* Removes the default border */
		transition:
			transform 0.2s ease,
			box-shadow 0.2s ease; /* Smooth transition for hover effects */
		animation: appear 0.5s forwards; /* Animate appearance */
	}

	.circle:hover {
		transform: scale(0.9); /* Slightly enlarge on hover */
		box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2); /* Increase shadow on hover */
	}

	.circle:active {
		transform: scale(0.95); /* Slightly shrink on click */
	}
</style>
