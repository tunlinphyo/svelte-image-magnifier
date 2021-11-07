<script>
	import Magnifier from 'svelte-image-magnifier'
	export let name;
</script>

<main>
	<div class="container">
		<section>
			<Magnifier image="/emma.jpeg" largeImage="/emma.jpeg" />
		</section>
		<section>
			<h1>Hello {name}!</h1>
			<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
		</section>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	.container {
		width: 100%;
		display: grid;
		grid-template-columns: 1fr 1fr;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>