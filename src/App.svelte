<script>
	export let name;
	let world = "Tinnakorn";
	let src   = 'assets/image/svelte.png';
</script>

<style>
	h1 {
		color: purple;
		font-family: 'Comic Sans MS';
		font-size: 2em;
	}
</style>

<h1>Hello {name}!</h1>
<br>
<h1>Hello {world.toUpperCase()}!</h1>
<br>
<img {src} alt="{name} dances.">
