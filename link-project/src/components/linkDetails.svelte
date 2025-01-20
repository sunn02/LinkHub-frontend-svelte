<script>
    import { onMount, createEventDispatcher } from 'svelte';
    import { fetchLinkDetails, voteLink, commentLink } from '../api.js';

    const dispatch = createEventDispatcher();
    export let id;
    let link = null;
    let comments = [];
    let newComment = '';
  
    async function loadDetails() {
      const data = await fetchLinkDetails(id);
      link = data.link;
      comments = data.comments;
    }
  
    async function handleVote() {
      const updatedLink = await voteLink(id);
      link.votes = updatedLink.votes;  
    }
  
    async function handleCommentSubmit(event) {
      event.preventDefault();
      await commentLink(id, newComment);
      newComment = '';
      loadDetails()
    }
  
    onMount(() => {
      loadDetails();
    });
</script>
  
  {#if link}
    <h1>Detalles</h1>
    <p><strong>Votos:</strong> {link.votes}</p>
    <button on:click={handleVote}>Votar</button>
    <p><strong>Comentarios:</strong></p>
    <ul>
      {#each comments as comment}
        <li>{comment.content}</li>
      {/each}
    </ul>
    
    <form on:submit={handleCommentSubmit}>
      <textarea bind:value={newComment} placeholder="Escribe tu comentario aquí"></textarea>
      <button type="submit">Enviar</button>
    </form>
  <button on:click= {() => dispatch('home')}>Volver</button>  
  {/if}
  