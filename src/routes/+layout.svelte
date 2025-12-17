<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import GridOverlay from '$lib/GridOverlay.svelte';

	let { children } = $props();

	import '../styles/index.scss';
</script>

<svelte:head>
	<link rel="icon" href={favicon} />

	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous">
	<link href="https://fonts.googleapis.com/css2?family=Hanken+Grotesk:ital,wght@0,100..900;1,100..900&family=STIX+Two+Text:ital,wght@0,400..700;1,400..700&display=swap" rel="stylesheet">
</svelte:head>

<GridOverlay />
{@render children()}
