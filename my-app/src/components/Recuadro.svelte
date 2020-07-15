<script>
export let persona;
export let cleanPersona;
export let loader;
export let direccion;

</script>

<style>

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
</style>

<div class="Recuadro">
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

</div>
