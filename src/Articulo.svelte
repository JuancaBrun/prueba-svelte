<script>
    export let articulo = {
        nombre: "",
        precio: 0,
    };
</script>

<br />
<input
    type="text"
    name="nombre"
    id="nombre"
    placeholder="Nombre"
    bind:value={articulo.nombre}
/><br />
<input
    type="number"
    name="precio"
    id="precio"
    placeholder="Precio"
    bind:value={articulo.precio}
/>
<br />
<slot />
