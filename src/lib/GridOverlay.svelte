<script lang="ts">
	// Grid overlay component that displays dotted lines for every other column
	// This sits behind all content as a visual guide
</script>

<div class="grid-overlay">
	{#each Array(10) as _, i}
		<div class="grid-overlay__column"></div>
	{/each}
</div>
