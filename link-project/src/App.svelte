<script>
	import { writable } from 'svelte/store';
	import Home from './components/home.svelte';
	import LinkDetails from './components/linkDetails.svelte';
	import LinkForm from './components/linkForm.svelte';

	const currentPage = writable('home');
	const currentLinkId = writable(null);

	function goTo(page, id = null) {
		currentPage.set(page);
		currentLinkId.set(id);
	}
</script>


<main>
    {#if $currentPage === 'home'}
        <Home 
            on:details={(event) => goTo('details', event.detail.id)} 
            on:newLink={() => goTo('newLink')} 
        />
    {:else if $currentPage === 'details'}
        <LinkDetails id={$currentLinkId} />
    {:else if $currentPage === 'newLink'}
        <LinkForm on:home={() => goTo('home')} />
    {/if}
</main>


