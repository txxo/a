<script>
	export let card
	export let handleChoice
	export let flipped
	const handleClick = () => {
		handleChoice(card)
	}
</script>

<div class="card" >
	<div class={flipped?'flipped':''}>
		<img class="front" src={card.src} alt="card front" />
		<img on:click={handleClick} class="back" src="/img/cover.png" alt="card back" />
	</div>
</div>

<style>
  .card{
    position: relative;
  }

	.card img {
		width: 100%;
		display: block;
		border: 2px solid #fff;
		border-radius: 6px;
	}

  .card .front {
    transform: rotateY(90deg);
    position: absolute;

  }


  .flipped .front {
    transform: rotateY(0deg);
  }
</style>
