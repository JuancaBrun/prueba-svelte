<script>
    import {onMount} from 'svelte';
    import Buscador from './Buscador.svelte';
    const URL = 'https://tiendabackend.fly.dev/api/articulos/';
    let data = [];
    let inputBusqueda = "";

    let getArticulos = async () => {
        const response = await fetch(URL);
        data = await response.json();
    }

    onMount(getArticulos);

    $: datosFiltrados = data.filter( articulo => RegExp(inputBusqueda, "i").test(articulo.nombre) );
</script>

<h1>Artículos</h1>

<Buscador bind:patron={inputBusqueda}/>

<ul>
{#each datosFiltrados as articulo}
    <li>{articulo.nombre}:   {articulo.precio}</li>
{/each}
</ul>