<script>
	export let name;
	let name1 = 'jimmy';
    function handleClick(){
		if(name1==='jimmy'){
			name1="Deepa"
		}else{
			name1='jimmy'
		}
	}
    function inputText(e){
       name1 = e.target.value
	}
    let firstName = 'Albin'
	let LastName = 'Gogul'
	$: fullName =`${firstName} ${LastName}`
	import Curd from './Curd.svelte';
</script>

<main>
	<Curd/>
	<h1>Hello {name1}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	<p>Name- {fullName} </p>
	<input type="text" placeholder="input value" bind:value={name}>
	<button on:click={handleClick}>click to change name</button>
	<input type="text" placeholder="iput text changr the name " on:input={inputText}>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
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