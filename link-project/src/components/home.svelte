<script>
    import { createEventDispatcher, onMount } from 'svelte';
    import { fetchLinks } from '../api.js';

    const dispatch = createEventDispatcher();
    let links = [];

    async function loadLinks() {
        links = await fetchLinks();
    }

    onMount(loadLinks);
</script>

<div>
    <div>
        {#each links as link}
            <div class="link">
                <h3>{link.title}</h3>
                <p>{link.url}</p>
                <button on:click={() => dispatch('details', { id: link._id })}>Ver Detalles</button>
            </div>
        {/each}
    </div>
</div>