<script>
	import { writable } from 'svelte/store'
	import SingleCard from '../components/singleCard.svelte'

	const cards = writable([])
	const turns = writable(0)
	let choiceOne = null
	let choiceTwo = null
  let flag = false
	const cardImgs = [
		{ src: '/img/helmet-1.png', matched: false },
		{ src: '/img/potion-1.png', matched: false },
		{ src: '/img/ring-1.png', matched: false },
		{ src: '/img/scroll-1.png', matched: false },
		{ src: '/img/shield-1.png', matched: false },
		{ src: '/img/sword-1.png', matched: false }
	]

	const shuffleCards = () => {
		const shuffledCards = [...cardImgs, ...cardImgs]
			.sort(() => Math.random() - 0.5)
			.map((card) => ({ ...card, id: Math.random() }))
		cards.set(shuffledCards)
		turns.set(0)
	}
	const handleChoice = (card) => {

		choiceOne ? (choiceTwo = card) : (choiceOne = card)
    cpr(choiceTwo,choiceOne)

	}


  const cpr = (a,b)=>{
    if(a&&b){
      if(a.src==b.src){
        flag = true
        resetCard()
      }
    }
  }

  const resetCard = ()=>{
    choiceOne=null
    choiceTwo=null
  }

  



</script>

<div class="App">
	<h1>Magic Match</h1>
	<button on:click={shuffleCards}>New Game{$turns}</button>

	<div class="card-grid">
		{#each $cards as card (card.id)}
			<SingleCard
				flipped={card == choiceTwo || card == choiceOne}
				handleChoice={() => handleChoice(card)}
				{card}
			/>
		{/each}
	</div>
</div>

<style>
	.App {
		max-width: 860px;
		margin: 40px auto;
	}
	button {
		background: none;
		border: 2px solid #fff;
		padding: 6px 12px;
		border-radius: 4px;
		color: #fff;
		font-weight: bold;
		cursor: pointer;
		font-size: 1em;
		margin-bottom: 30px;
	}
	button:hover {
		background: #c23866;
		color: #fff;
	}

	.card-grid {
		margin-top: 40;
		display: grid;
		grid-template-columns: 1fr 1fr 1fr 1fr;
		grid-gap: 20px;
	}
</style>
