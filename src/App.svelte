<script>
	import Nested from './Nested.svelte';
	export let name;
	let world  = "Tinnakorn";
	let src    = 'assets/image/svelte.png';
	let string = `this string contains some <strong>HTML!!!</strong>`;

	let count = 0;

	function handleClick() {
		count += 1;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {name}!</h1>

<br>

<h1>Hello {world.toUpperCase()}!</h1>

<br>

<img {src} alt="{name} dances." width="10%">

<!-- import component -->
<Nested/>

<p>{@html string}</p>

<button on:click={handleClick}>
	Clicked {count} {count === 1 ? 'time' : 'times'}
</button>
