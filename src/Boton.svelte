<script>
    import { onMount } from "svelte";
    import { data } from "./store";

    export let tipo = "insertar";
    export let documento = {};

    import { getContext } from "svelte";
    const URL = getContext("URL");

    let handler = () => {};

    function insertar() {
        let opciones = {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        };
        fetch(URL.articulos, opciones)
            .then((res) => res.json())
            .then((datos) => {
                $data = [...$data, datos];
            })
            .catch((error) => console.log(error));
    }

    function modificar() {
        console.log("modificar");
        let opciones = {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        };
        fetch(URL.articulos + "/" + documento._id, opciones)
            .then((res) => res.json())
            .then((datos) => console.log(datos))
            .catch();
    }

    function eliminar() {
        console.log("eliminar");
        let opciones = {
            method: "DELETE",
        };
        fetch(URL.articulos + "/" + documento._id, opciones)
            .then((res) => res.json())
            .then((datos) => ($data = $data.filter((x) => x._id !== datos._id)))
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
