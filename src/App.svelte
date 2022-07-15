<!---------------- JAVASCRIPT -------------------->
<script>
  let result = []
  let search = ''
  let Abilities = []

	async function getPokemon () {
		const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${search}`, {
			method: 'GET',
      headers: {
        'Content-Type': 'application/json'
      }
		})
    console.log(res)
		result = await res.json()
    Abilities = result.abilities.map(ability => ability.ability.name.toUpperCase())
	}
</script>

<!-------------- HTML ---------------------------->
<div class="container">
  <h1>PokeApp</h1>
  <input type="text" placeholder="Search for a Pokemon" on:input={e => (search = e.target.value.toLowerCase())} on:keyup={e => (e.key === 'Enter' ? getPokemon() : null)} class="search" />
  <button on:click={getPokemon} class="btn btn-secondary">Search</button>
  {#if result && result.name}
    <div class="card">
      <h2>{result.name.toUpperCase()}</h2>
      <img src={result.sprites.other.home.front_default} alt={result.name} />
      <span>
        <p>ABILITIES: {Abilities.join(', ')}</p>
        <p>HEIGHT: {result.height}</p>
        <p>WEIGHT: {result.weight}</p>
        <p>TYPE: {result.types.map(type => type.type.name.toUpperCase()).join(', ')}</p>
      </span>
    </div>
  {/if}
</div>

<!-------------- CSS ------------------------------>

<style>
  .search {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
  }
  .card {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .card h2 {
    font-size: 40px;
    margin-bottom: 10px;
    text-align: center;
    font-weight: 600;
  }
  h1 {
    text-align: center;
    font-weight: 600;
    font-size: 80px;
    margin: 20px 0;
    }
  .container {
    align-items: center;
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 100vh;
  }
  .card img {
    width: 25%
  }
  @media (max-width: 650px) {
    .card img {
      width: 50%
    }
  }
  button {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
    margin: 10px;
    width: 100%;
  }
</style>
