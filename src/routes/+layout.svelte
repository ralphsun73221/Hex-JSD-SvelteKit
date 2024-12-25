<script lang="ts">
  import Nav from "$lib/Nav.svelte";
	let { children } = $props();
</script>

<Nav />

{@render children()}

<style>
</style>
