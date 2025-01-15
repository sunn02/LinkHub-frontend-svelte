<script>
    import { onMount } from 'svelte';
    import { fetchLinkDetails, voteLink, commentLink } from '../api.js';

    export let id;
    let link = null;
    let newComment = '';

    async function loadDetails() {
        link = await fetchLinkDetails(id);
        console.log(link)
    }

    async function handleVote() {
        const updatedLink = await voteLink(id);
        link = updatedLink.link;
        loadDetails();
    }

    async function handleCommentSubmit(event) {
        event.preventDefault();
        await commentLink(id, newComment);
        newComment = '';
        loadDetails();
    }

    onMount(loadDetails);
</script>

<div>
    {#if link}
        <div class="link">
            <span>Votos: {link.votes}</span>
            <button on:click={() => handleVote(1)}>Votar</button>
        </div>
        <div>
            {#each link.comments as comment}
                <p>{comment.content}</p>
            {/each}
        </div>
        <form on:submit={handleCommentSubmit}>
            <textarea bind:value={newComment} placeholder="Nuevo comentario"></textarea>
            <button type="submit">Enviar</button>
        </form>
    {/if}
</div>