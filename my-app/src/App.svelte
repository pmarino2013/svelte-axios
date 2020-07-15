<script>
//importo axios 
import axios from 'axios';
//importo del ciclo de vida el onMount
import {onMount} from 'svelte';

	
	let datos=[];
	let persona={};
	let loader=false;
	let direccion={};
	
	//Cuando se monta el componente
	onMount(()=>{
		getData();
	})

	//función para traer la data
	const getData= async()=>{
		const {data}= await axios.get('https://jsonplaceholder.typicode.com/users')
		try {
			datos=data;
					
		} catch (error) {
			console.error(error)
		}
	}
//Función para consultar un usuario
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

const cleanPersona=()=>{
	persona={};
}
	

</script>

<main>
	<h1>Axios en Svelte</h1>
	<h3>Haga clic en un nombre para ver mas detalles</h3>
	<div class="lista">
		<ul>
		{#each datos as dato (dato.id)}
			<li class="puntero" on:click={getUser(dato.id)}>
				{dato.name}
			</li>
		{/each}
		</ul>
	</div>
	{#if persona.length>0}
	<section id="recuadro">
	<div class="container">
		<div class="boton">
			<span class="btn-close" on:click={cleanPersona}></span>
		
		</div>
		<section id="datos_persona"> 
			<h3>{persona[0].name}</h3>
			<span><strong>Direccion: </strong> {direccion.street} {direccion.suite}</span>
		
		</section>
	</div>
	</section>
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
	.lista{
		display: flex;
		justify-content:center;
	}
	ul{
		padding: 0;
		margin: 10, 0;
	}
	.puntero{
		cursor: pointer;
		


	}
	.puntero:hover{
		color:#ff3e00;
	}
	li{
		list-style: none;
	}
	#recuadro{
	    width: 100%;
		display: flex;
		justify-content: center;
	}
.container{
	
	width: 300px;
	height: 150px;
	text-align: center;
	border:solid 1px burlywood;
}
.boton{
	display: flex;
	flex-direction: row-reverse;
	height: 40px;
	
	background-color:black;
	
}
.btn-close{
	
	width: 20px;
	height: 20px;
	margin: 10px;
	
	background-color: #ff3e00;
	border-radius: 10px;
	color:white;
	border:0;
	cursor: pointer;
	
}
#datos_persona{
	display: inline-block;
width: 100%;
	margin-top: 0;
	padding-top: 0;

}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>