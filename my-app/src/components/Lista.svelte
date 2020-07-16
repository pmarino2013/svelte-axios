<script>
export let datos;
export let getUser;

</script>

<style>
.Lista{
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
</style>

<div class="Lista">
    	<ul>
		{#each datos as dato (dato.id)}
			<li class="puntero" on:click={getUser(dato.id)}>
				{dato.name}
			</li>
		{/each}
		</ul>

</div>