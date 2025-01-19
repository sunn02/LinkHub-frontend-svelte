<script>
    import { createEventDispatcher, onMount } from 'svelte';
    import { fetchLinks } from '../api.js';

    const dispatch = createEventDispatcher();
    let links = [];
    let filter = ''; 

    async function loadLinks(tagFilter = '') {
        links = await fetchLinks(tagFilter); 
    }

    onMount(() => loadLinks());

    function handleFilterChange(event) {
        filter = event.target.value; // Actualiza el filtro al escribir
        loadLinks(filter); // Carga los enlaces filtrados
    }

</script>

<div>
    <div>
        <!-- Campo de entrada para el filtro -->
        <input
            type="text"
            placeholder="Filtrar por etiqueta"
            bind:value={filter}
            on:input={handleFilterChange}
        />
    </div>

    <div>
        {#if links.length > 0}
            {#each links as link}
                <div class="link">
                    <h3>{link.title}</h3>
                    <p>{link.url}</p>
                    <p>{link.description}</p>
                    <p><strong>Tags:</strong> {link.tags}</p>
                    <button on:click={() => dispatch('details', { id: link._id })}>Ver Detalles</button>
                </div>
            {/each}
        {:else}
            <p>No se encontraron enlaces.</p>
        {/if}
    </div>
    <button on:click= {() => dispatch('newLink')}>Añadir Enlace</button>

</div>


