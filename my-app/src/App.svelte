<script>
import Lista from './components/Lista.svelte';
import Recuadro from './components/Recuadro.svelte';

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
	
	<Lista getUser={getUser} datos={datos} />

	<Recuadro persona={persona} cleanPersona={cleanPersona} direccion={direccion} loader={loader} />
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