<script>
    import { onMount } from "svelte";

    export let tipo = "insertar";
    export let documento = {};

    import { getContext } from "svelte";
    let URL = getContext("URL");

    let handler = () => {};

    function insertar() {
        console.log("insertar");
        let opciones = {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        };
        fetch(URL.articulos, opciones)
            .then((res) => res.json())
            .then((datos) => console.log(datos))
            .catch((error) => console.log(error));
    }

    function modificar() {
        console.log("modificar");

        // let opciones = {
        //     method: "PUT",
        //     headers: { "Content-Type": "application/json" },
        //     body: {
        //         nombre: document.getElementById("nombre").value,
        //         precio: document.getElementById("precio").value,
        //     },
        // };
        // fetch(URL.articulos, opciones)
        //     .then((res) => res.json())
        //     .then((datos) => console.log(datos))
        //     .catch();
    }

    function eliminar() {
        console.log("eliminar");
        let opciones = {
            method: "DELETE",
            headers: { "Content-Type": "application/json" },
            body: {
                nombre: document.getElementById("nombre").value,
                precio: document.getElementById("precio").value,
            },
        };
        fetch(URL.articulos, opciones)
            .then((res) => res.json())
            .then((datos) => console.log(datos))
            .catch();
    }

    function setup() {
        switch (tipo) {
            case "insertar":
                handler = insertar;
                break;
            case "modificar":
                handler = modificar;
                break;
            case "eliminar":
                handler = eliminar;
                break;
            default:
        }
    }

    onMount(setup);
</script>

<input
    type="button"
    value={tipo == "insertar"
        ? "Enviar 💩"
        : tipo == "modificar"
        ? "Modificar"
        : "Eliminar"}
    on:click={handler}
/>
