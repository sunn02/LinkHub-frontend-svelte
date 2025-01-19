<script>
    import { createEventDispatcher } from 'svelte';
    import { saveLink } from "../api";

    const dispatch = createEventDispatcher();
    let titleInput = "";
    let urlInput = "";
    let descriptionInput = "";
    let tagsInput = "";

    async function save() {
        const newLink = {
            title: titleInput,
            url: urlInput,
            description: descriptionInput,
            tags: tagsInput.split(','), 
        };

        try {
            await saveLink(newLink);
            console.log("Enlace guardado con éxito");
            dispatch('home');
            titleInput = "";
            urlInput = "";
            descriptionInput = "";
            tagsInput = "";
        } catch (error) {
            console.error("Error al guardar el enlace:", error);
            alert("Ocurrió un error al guardar el enlace. Por favor, inténtalo nuevamente.");
        }
    }
</script>

<!-- Formulario -->
<form on:submit|preventDefault={save}>
    <label for="title">Título:</label>
    <input
        id="title"
        type="text"
        bind:value={titleInput}
        placeholder="Ingresa el título"
        required
    />

    <label for="url">URL:</label>
    <input
        id="url"
        type="url"
        bind:value={urlInput}
        placeholder="Ingresa la URL"
        required
    />

    <label for="description">Descripción:</label>
    <textarea
        id="description"
        bind:value={descriptionInput}
        placeholder="Ingresa una descripción"
        required
    ></textarea>

    <label for="tags">Etiquetas (separadas por comas):</label>
    <input
        id="tags"
        type="text"
        bind:value={tagsInput}
        placeholder="ejemplo1, ejemplo2"
    />

    <button type="submit">Guardar</button>
</form>

