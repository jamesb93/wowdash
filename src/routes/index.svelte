<script>
	import Character from '$lib/Character.svelte';
</script>

<main>
	<div class="character-container">
	<Character
		name="Boogalumps"
		realm="Illidan"
	/>

	<Character
		name="Havefuntoday"
		realm="Illidan"
	/>

	<Character
		name="Willywong"
		realm="Illidan"
	/>

	<Character
		name="Huntydumpty"
		realm="Saurfang"
	/>

	<Character
		name="Soggysoup"
		realm="Saurfang"
	/>

	<Character
		name="Liquidchalk"
		realm="Saurfang"
	/>
	</div>

</main>

<style lang="scss">
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
	}

	.character-container {
		display: flex;
		flex-direction: row;
		flex-wrap:wrap;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 100;
		line-height: 1.1;
		margin: 4rem auto;
		max-width: 14rem;
	}

	p {
		max-width: 14rem;
		margin: 2rem auto;
		line-height: 1.35;
	}

	@media (min-width: 480px) {
		h1 {
			max-width: none;
		}

		p {
			max-width: none;
		}
	}
</style>
