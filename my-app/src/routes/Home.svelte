<script>
import {loginState} from '../store/store.js';

import Lista from '../components/Lista.svelte';
import Recuadro from '../components/Recuadro.svelte';
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

const setLogin=()=>{

if($loginState){
	loginState.set(false);
}else{

	loginState.set(true);
}

	
}

const cleanPersona=()=>{
	persona={};
}
	

</script>

<div class="Home">

	<h1>Axios en Svelte</h1>
	<button class="btn-login" on:click={setLogin}>{$loginState?'Logout':'Login'}</button>
	{#if $loginState }
	
	<h3>Haga clic en un nombre para ver mas detalles</h3>
	
	<Lista {getUser} {datos} />

	<Recuadro {persona} {cleanPersona} {direccion} {loader} />

	{:else}
		<h3>No está logueado</h3>
		
	
	{/if}

</div>

<style>
	.Home {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	.btn-login{
		width: 100px;
		height: 40px;
		border:none;
		padding: 0 5px 5px 5px;
		margin: 0;
		background-color: #ff3e00;
		color:white;
		border-radius: 20px;
		text-align: center;
		display:inline-block;
		cursor: pointer;
	}
	.btn-login:active{
		background-color: #752003;
		color:white;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	
	@media (min-width: 640px) {
		.Home {
			max-width: none;
		}
	}
</style>