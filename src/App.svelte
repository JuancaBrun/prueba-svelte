<script>
    import Clientes from "./Clientes.svelte";
import Nav from "./Nav.svelte";
import {Router} from 'svelte-routing';
    import Articulos from "./Articulos.svelte";
    import Contenido from "./Contenido.svelte";
    import Footer from "./Footer.svelte";


</script>

<Router>
	<Nav/>
	<Contenido />
	<Footer />
</Router>


<style>
:global(body){
	margin: 0 auto;
	padding: 0;
	background-color: pink;
	color: blue;
}

:global(h1){
	text-align: center;
}

</style>