<script>

let movies = [ ];

let search = ""; 

function findMovie() {
	fetch("https://api.themoviedb.org/3/search/movie?language=pt-br&sort_by=popularity&include_video=1&api_key=ab9784d6bd2d7cf6dbf8a2840a51a9bc&query=" + search)
	.then(rest => rest.json())
	.then( rest => {
		console.log(rest);
		movies = rest.results;
	})
}
</script>

<style>

.conteudo {
	max-width: 800px;
	margin: 0 auto;
	padding: 0 20px;
}

.input {
	border: 0;
	margin-bottom: 32px;
	padding: 12px 32px;
	border-radius: 200px 200px;
	background-color: #ebebeb;
	width: 100%;
	outline: 0;
	font-family: 'Lato', sans-serif;
}

.tituloPagina {
	text-align: center;
	font-family: 'Abel', sans-serif;
	color: #00e8e4;
	background-color: #116193;
	padding: 20px;
	margin: 0px 0px 20px 0px;
}

.tituloFilme {
	text-align: left;
	font-family: 'Abel', sans-serif;
	color: #00e8e4;
	background-color:#116193;
	padding: 0px 0px 0px 90px;
	margin: 0px;
}

.lançamento {
	font-family: 'Lato', sans-serif;
	color: rgb(73, 73, 73);
	background-color: #ebebeb;
	padding: 0px 0px 10px 90px;
	margin: 0px;
	position: relative;
	top: -58px;
}

.sinopse {
	font-family: 'Lato', sans-serif;
	color: rgb(73, 73, 73);
	background-color: #ebebeb;
	border: 20px;
	margin: 0px;
	padding: 0px 0px 10px 10px;
	position: relative;
	top: -58px;
}

.pontuacao {
	font-family: 'Abel', sans-serif;
	font-size: 25px;
	text-align: center;
	color: #00e8e4;
	background-color: #116193;
	padding: 0px;
	margin: 0px;
	border: 4px solid #00e8e4;
	border-radius: 200px 200px;
	width: 50px;
	height: 50px;
	position: relative;
	top: -30px;
	left: 20px;
	z-index: 2;
	line-height: 50px;
}

:global(body) {
   margin: 0;
   padding: 0;
}

.todosOsFilmes {
	display: flex;
	justify-content: center;
	background-color: #ebebeb;
	margin-bottom: 20px;
}

.folder {
	max-height: 350px;
	width: 25%;
	object-fit: cover;
	object-position: center;
}

.info {
	width: 75%;
}

@media(max-width: 600px) {
	.todosOsFilmes {
		flex-direction: column;
	}
	.info {
		width: 100%;
	}
	.folder {
		width: 100%; 
		max-width: 100%; 
		max-height: 200px;
	}
}

</style>

<h1 class="tituloPagina">Movies</h1>

<div class="conteudo">
	<form on:submit|preventDefault={findMovie}>
		
		<input type="text" class="input" placeholder="Busque um filme por nome." bind:value = {
			search
		}>

		
	</form>

	{#each movies as movie }
		<div class="todosOsFilmes">
			<img class="folder" src="https://image.tmdb.org/t/p/w600_and_h900_bestv2{movie.poster_path}" alt="poster do filme">
			<div class="info">
				<h1 class="tituloFilme">{movie.title}</h1>
				<p class="pontuacao">{movie.vote_average*10}%</p>
				<p class="lançamento">{movie.release_date}</p>
				<p class="sinopse">{movie.overview}</p>
			</div>

		</div>
		
	{/each}
</div>
