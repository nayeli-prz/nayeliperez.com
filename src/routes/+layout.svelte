<script lang="ts">
	import favicon from '$lib/assets/favicon-v2.svg';
	import GridOverlay from '$lib/GridOverlay.svelte';

	let { children } = $props();

	import '../styles/index.scss';
</script>

<svelte:head>
	  <title>Nayeli Pérez | Designer</title>

	<link rel="icon" href={favicon} />

	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous">
	<link href="https://fonts.googleapis.com/css2?family=Hanken+Grotesk:ital,wght@0,100..900;1,100..900&family=STIX+Two+Text:ital,wght@0,400..700;1,400..700&display=swap" rel="stylesheet">

	<!-- Privacy-friendly analytics by Plausible -->
	<script async src="https://plausible.io/js/pa-X1WqC3rs4vcSmZ_agNhBJ.js"></script>
	<script>
	window.plausible=window.plausible||function(){(plausible.q=plausible.q||[]).push(arguments)},plausible.init=plausible.init||function(i){plausible.o=i||{}};
	plausible.init()
	</script>


</svelte:head>

<GridOverlay />
{@render children()}
