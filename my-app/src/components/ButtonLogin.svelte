<script>
import {loginState} from '../store/store.js';

const setLogin=()=>{

if($loginState){
	loginState.set(false);
}else{

	loginState.set(true);
}

	
}
</script>

<style>
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
	.btn-logout{
		width: 100px;
		height: 40px;
		border:none;
		padding: 0 5px 5px 5px;
		margin: 0;
		background-color: dimgrey;
		color:white;
		border-radius: 20px;
		text-align: center;
		display:inline-block;
		cursor: pointer;
	
	}
	.btn-logout:active{
		background-color: rgb(58, 56, 56);
		color:white;
	}
	
</style>

<div class="ButtonLogin">
<button class={$loginState ? 'btn-logout': 'btn-login'}  on:click={setLogin}>{$loginState ? 'Logout':'Login'}</button>
</div>