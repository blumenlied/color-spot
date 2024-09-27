<script>
	import Board from '../components/Board.svelte';
</script>

<svelte:head>
	<title>racer</title>
</svelte:head>

<main>
	<h1>professional racist</h1>
	<Board />
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		margin: 0;
		color: #ff3e00;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
