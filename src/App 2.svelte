<script>

	import { onMount } from 'svelte';
	
	let klasse = "faller"
	
	let tall1 = 0
	let tall2 = 0
	$: fasit = tall1 * tall2
	let svar = ""
	let theGameIsOn = true
	$: riktigsvar = (fasit === svar)
	$: regnestykke = `${tall1} x ${tall2}`
	let poeng = 0

	onMount(() => {
		lagNyeTall();

	});
	
	const lagNyeTall = () => {
		tall1 =  Math.ceil(Math.random() * 10)
		tall2 =  Math.ceil(Math.random() * 10)
	}

	const restart = () => {
		theGameIsOn = true;
		poeng = 0;
		svar = "";
		klasse = "";
		lagNyeTall();
		setTimeout( () => { klasse = "faller" }, 50 )
	}
	
	const sjekkSvar = () => {
		if(riktigsvar && theGameIsOn) {
			lagNyeTall()
			svar = ""	
			klasse = ""
			poeng++
			setTimeout( () => { klasse = "faller" }, 50 )
		}
		
	}
	
	const gameOver = () => {
		theGameIsOn = false
		console.log("GAME OVER")

		if (poeng == 0) {
			alert(`GAME OVER 😫 Ingen poeng!`);
		} else {
			alert(`GAME OVER 😫 Du klarte ${poeng}🤩`);
		}
	
	}

	
</script>


<section>
	<header>
		<div>
			<p class="poeng-overskrift">Poeng</p>
			<p class="poeng">{poeng}</p>
		</div>
		<div>
			<p class="poeng-overskrift">Highscore</p>
			<p class="poeng">{poeng}</p>
		</div>
	</header>	
	
	<main>
		<div on:animationend={gameOver} class="{klasse}">{regnestykke}</div>	
	</main>
	
	<footer>
		<input type="number" placeholder="Skriv inn tall" bind:value={svar} on:input={sjekkSvar}>
		<button class="button" on:click={restart} type="Restart" value="Restart">Restart</button>

		
	</footer>
	
</section>

<style>

	*{
		margin: 0;
		font-family: Arial, Helvetica, sans-serif;
	}


	.faller{
		animation: fallNed 5s linear forwards;
	}

	.poeng {
		font-weight: 700;
		text-align: center;
	}

	.poeng-overskrift {
		font-size: 12pt;
		text-align: center;
	}

	.poeng{
		text-align: center;
		font-size: 2rem;
		
	}

	@keyframes fallNed{
		to{
			transform: translateY(500px);
		}
	}

 	main div {
	width: 200px;
	height: 50px;
	line-height: 50px;
	margin: 10px auto;
	background-color: #FBD000;
	text-align: center;
	font-size: 2rem;
	border-radius: 4px


	}

	section{
		display: grid;
		grid-template-rows:  auto 450px auto;
		font-size: 5rem;
		
	}

	footer{
		background-color: #43B047;
		padding: 20px;
	}


	.button {
		background-color: #4CAF50; /* Green */
		color: white;
		transition-duration: 0.4s;
		padding: 44px;
		width: 400px;
		font-size: 20px;
		letter-spacing: 4px;
		cursor: pointer;
		border: 1px solid black
	}

	input{
		padding: 44px;
		width: 50%;
		font-size: 20px;
		letter-spacing: 4px;
		border: 1px solid black;
	
	}

	header{
		background-color: #6a87fe;
		color: white;
		padding: 0.8rem;
		display: grid; 
		grid-template-columns: 1fr 1fr;	
		border: 1px solid #0e1427
	}

	main{
		background-image: url("https://i.pinimg.com/originals/dc/8d/ef/dc8def609c27f9123c4f61a83a3b93bd.jpg");
		background-repeat: no-repeat;
		background-size: cover;
		background-position: bottom;

	}
	
</style>