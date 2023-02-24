<script>
    import { onMount } from "svelte";
    import { getContext } from "svelte";
    import { data } from "./store";
    import Buscador from "./Buscador.svelte";
    import Articulo from "./Articulo.svelte";
    import Boton from "./Boton.svelte";
    let articuloInsertar = {};
    let inputBusqueda = "";

    const URL = getContext("URL");

    let getArticulos = async () => {
        const response = await fetch(URL.articulos);
        $data = await response.json();
    };

    onMount(getArticulos);

    $: datosFiltrados = $data.filter((articulo) =>
        RegExp(inputBusqueda, "i").test(articulo.nombre)
    );
</script>

<h1>Artículos</h1>
<Buscador bind:patron={inputBusqueda} />

<hr />
<Articulo articulo={articuloInsertar}>
    <Boton documento={articuloInsertar} />
</Articulo>

<ul>
    {#each datosFiltrados as articulo}
        <Articulo {articulo}>
            <Boton tipo="modificar" bind:documento={articulo} />
            <Boton tipo="eliminar" bind:documento={articulo} />
        </Articulo>
    {/each}
</ul>
