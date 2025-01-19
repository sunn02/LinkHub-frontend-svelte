<script>
	import { writable } from 'svelte/store';
	import Home from './components/home.svelte';
	import LinkDetails from './components/linkDetails.svelte';

	const currentPage = writable('home');
	const currentLinkId = writable(null);

	function goTo(page, id = null) {
		currentPage.set(page);
		currentLinkId.set(id);
	}
</script>


<main>
	{#if $currentPage === 'home'}
		<Home on:details={(event) => goTo('details', event.detail.id)} />
	{:else if $currentPage === 'details'}
        <LinkDetails id={$currentLinkId} />
	{/if}
</main>

