<script>
  import { loginState } from "../store/store.js";

  import axios from "axios";

  let correoUser = "";
  let usuario = [];
  let alerta = false;

  const validar = async email => {
    if ($loginState) {
      loginState.set(false);
    } else {
      const respuesta = await axios.get(
        `https://jsonplaceholder.typicode.com/users?email=${email}`
      );

      try {
        usuario = respuesta.data;
        console.log(usuario);
        if (usuario.length > 0) {
          loginState.set(true);
          correoUser = "";
          alerta = false;
        } else {
          alerta = true;
        }
      } catch (error) {
        console.error(error);
      }
    }
  };

  const setLogin = () => {
    validar(correoUser);
    console.log(usuario);
    console.log(alerta);
  };
</script>

<style>
  .formulario {
    display: inline-block;
  }
  .formulario input {
    border-radius: 10px;
    text-align: center;
  }

  .btn-container {
    margin-top: 10px;
  }

  .btn-login {
    width: 100px;
    height: 40px;
    border: none;
    padding: 0 5px 5px 5px;
    margin: 0;
    background-color: #ff3e00;
    color: white;
    border-radius: 20px;
    text-align: center;
    display: inline-block;
    cursor: pointer;
  }
  .btn-login:active {
    background-color: #752003;
    color: white;
  }
  .btn-logout {
    width: 100px;
    height: 40px;
    border: none;
    padding: 0 5px 5px 5px;
    margin: 0;
    background-color: dimgrey;
    color: white;
    border-radius: 20px;
    text-align: center;
    display: inline-block;
    cursor: pointer;
  }
  .btn-logout:active {
    background-color: rgb(58, 56, 56);
    color: white;
  }

  .alert {
    color: #721c24;
    background-color: #f8d7da;
    border-color: #f5c6cb;
    padding: 10px;
    border-radius: 0.25rem;
  }
  .mensaje {
    margin-top: 1rem;
    padding: 0.75rem 1.25rem;
    margin-bottom: 1rem;
    border: 1px solid transparent;
    position: relative;
  }
</style>

<div class="ButtonLogin">
  <form>
    {#if !$loginState}
      <div class="formulario">

        <input
          type="text"
          placeholder="Ingrese su email"
          bind:value={correoUser} />

      </div>
    {/if}
    <div class="btn-container">
      <button
        type="button"
        class={$loginState ? 'btn-logout' : 'btn-login'}
        on:click={validar(correoUser)}>
        {$loginState ? 'Logout' : 'Login'}
      </button>
    </div>
    {#if alerta}
      <div class="mensaje">
        <span class="alert">Usuario no registrado</span>

      </div>
    {/if}
  </form>
</div>
