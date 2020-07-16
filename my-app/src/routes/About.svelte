<script>
import {loginState} from '../store/store.js';
</script>

<div class="About">
{#if $loginState}
    <h1>About</h1>
{:else}
<h2>Debe loguearse en la plataforma</h2>
{/if}
</div>