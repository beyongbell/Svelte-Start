<script>
	import Nested from './Nested.svelte';
	export let name;
	let world  = "Tinnakorn";
	let src    = 'assets/image/svelte.png';
	let string = `this string contains some <strong>HTML!!!</strong>`;

	let count  = 0;
	$: doubled = count * 2;

	$: if (count >= 10) {
		console.log(`the count is ${count}`);
		alert(`count is dangerously high!`);
		count = 9;
	}

	function handleClick() {
		count += 1;
	}

	let numbers = [1, 2, 3, 4];

	function addNumber() {
		numbers = [...numbers, numbers.length + 1];
	}

	$: sum = numbers.reduce((t, n) => t + n, 0);

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
<p>{count} doubled is {doubled}</p>


<p>{numbers.join(' + ')} = {sum}</p>
<button on:click={addNumber}>
	Add a number
</button>
