<script>
import axios from 'axios';
import {onMount} from 'svelte';

	export let name;
	let datos=[];
	let persona={};
	let loader=false;
	let direccion={};
	
	onMount(()=>{
		getData();
	})

	const getData= async()=>{
		const {data}= await axios.get('https://jsonplaceholder.typicode.com/users')
		try {
			datos=data;
					
		} catch (error) {
			console.error(error)
		}
	}

const getUser=async (user)=>{
	persona={};
	loader=true;
	const usuario = await axios.get(`https://jsonplaceholder.typicode.com/users?id=${user}`)
	try {
		persona=usuario.data;
		direccion=persona[0].address;
				
		loader=false;
	} catch (error) {
		console.error(error)
	}
}
	

</script>

<main>
	<h1>Hello {name}!</h1>
	<ul>
	{#each datos as dato (dato.id)}
		<li on:click={getUser(dato.id)}>
			{dato.name}
		</li>
	{/each}
	</ul>
	{#if persona.length>0}
	<div class="container">
		<h3>{persona[0].name}</h3>
		<span><strong>Direccion: </strong> {direccion.street} {direccion.suite}</span>
	</div>
	{:else}
		<h3>{loader ? 'Loading...': ''}</h3>
	{/if}
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
	li{
		list-style: none;
	}
.container{
	display:inline-block;
	
	width: 300px;
	height: 150px;
	border:solid 1px burlywood;
}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>