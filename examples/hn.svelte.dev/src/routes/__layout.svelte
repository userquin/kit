<script>
	import { page, navigating } from '$app/stores';
	import { onMount } from 'svelte';
	import { browser, dev } from '$app/env';
	import Nav from '$lib/Nav.svelte';
	import PreloadingIndicator from '$lib/PreloadingIndicator.svelte';
	import ThemeToggler from '$lib/ThemeToggler.svelte';
	import '../app.css';

	let SWPrompt;
	onMount(async () => {
		!dev && browser && (SWPrompt = (await import('$lib/SWPrompt.svelte')).default);
	});


	$: section = $page.path.split('/')[1];
</script>


<Nav {section}/>

{#if $navigating}
	<PreloadingIndicator/>
{/if}

<main>
	<slot></slot>
</main>

<ThemeToggler/>

{#if SWPrompt}
	<svelte:component this={SWPrompt}/>
{/if}

<style>
	main {
		position: relative;
		max-width: 56em;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>
