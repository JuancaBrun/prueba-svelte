<script>
	import Nav from "./Nav.svelte";
	import { Router } from "svelte-routing";
	import Contenido from "./Contenido.svelte";
	import Footer from "./Footer.svelte";
	import { setContext } from "svelte";

	const URL = {
		articulos: "https://tiendabackend.fly.dev/api/articulos",
		clientes: "https://tiendabackend.fly.dev/api/clientes",
	};

	setContext("URL", URL);
</script>

<Router>
	<Nav />
	<Contenido />
	<Footer />
</Router>

<style>
	:global(body) {
		margin: 0 auto;
		padding: 0;
		background-color: pink;
		color: blue;
	}

	:global(h1) {
		text-align: center;
	}
</style>
