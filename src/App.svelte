<script>
	import Nested from './Nested.svelte';
	import Interact from './Interact.svelte';
	import Info from './Info.svelte';
	import Thing from './Thing.svelte';
	import Inner from './Inner.svelte';
	import Outer from './Outer.svelte';
	import FancyButton from './FancyButton.svelte';

	export let name;

	let world  = "Tinnakorn";
	let src    = 'assets/image/svelte.png';
	let string = `this string contains some <strong>HTML!!!</strong>`;
	let firstname = 'world';

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

	const pkg = {
		name: 'svelte',
		version: 3,
		speed: 'blazing',
		website: 'https://svelte.dev'
	};

	let user = { loggedIn: false };

	function toggle() {
		user.loggedIn = !user.loggedIn;
	}

	let x = 7;

	let cats = [
		{ id: 'J---aiyznGQ', name: 'Keyboard Cat' },
		{ id: 'z_AbfPXTKms', name: 'Maru' },
		{ id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
	];

	let things = [
		{ id: 1, color: '#0d0887' },
		{ id: 2, color: '#6a00a8' },
		{ id: 3, color: '#b12a90' },
		{ id: 4, color: '#e16462' },
		{ id: 5, color: '#fca636' }
	];

	function handleClickThings() {
		things = things.slice(1);
	}

	let promise = getRandomNumber();

	async function getRandomNumber() {
		const res  = await fetch(`http://numbersapi.com/random/math`);
		const text = await res.text();
		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}

	function handleClickRandomNumber() {
		promise = getRandomNumber();
	}

	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

	function handleClickOnce() {
		alert('no more alerts')
	}

	function handleMessage(event) {
		alert(event.detail.text);
	}

	function handleClickButton() {
		alert('clicked');
	}

	let a = 1;
	let b = 2;

	let yes = false;

	let scoops = 1;
	let flavours = ['Mint choc chip'];

	let menu = [
		'Cookies and cream',
		'Mint choc chip',
		'Raspberry ripple'
	];

	function join(flavours) {
		if (flavours.length === 1) return flavours[0];
		return `${flavours.slice(0, -1).join(', ')} and ${flavours[flavours.length - 1]}`;
	}

</script>

<style>
	h1 {
		color: purple;
	}
	div { width: 20%; height: 20%; }
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

<Interact answer={42}/>
<Interact/>

<Info {...pkg}/>

{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{/if}

{#if !user.loggedIn}
	<button on:click={toggle}>
		Log in
	</button>
{/if}

{#if user.loggedIn}
	<button on:click={toggle}>
		Log out
	</button>
{:else}
	<button on:click={toggle}>
		Log in
	</button>
{/if}

{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}

<h1>The Famous Cats of YouTube</h1>
<ul>
	{#each cats as { id, name }, i}
		<li><a target="_blank" href="https://www.youtube.com/watch?v={id}">
			{i + 1}: {name}
		</a></li>
	{/each}
</ul>

<button on:click={handleClickThings}>
	Remove first thing
</button>

{#each things as thing}
	<Thing current={thing.color}/>
{/each}


<button on:click={handleClickRandomNumber}>
	generate random number
</button>

{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

<button on:click|once={handleClickOnce}>
	Click me
</button>

<div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div>

<div on:mousemove="{e => m = { x: e.clientX, y: e.clientY }}">
	The mouse position is {m.x} x {m.y}
</div>

<Inner on:message={handleMessage}/>

<Outer on:message={handleMessage}/>

<FancyButton on:click={handleClickButton}/>

<br>
<input bind:value={firstname}>

<h1>Hello {firstname}!</h1>

<label>
	<input type=number bind:value={a} min=0 max=10>
	<input type=range bind:value={a} min=0 max=10>
</label>

<label>
	<input type=number bind:value={b} min=0 max=10>
	<input type=range bind:value={b} min=0 max=10>
</label>

<p>{a} + {b} = {a + b}</p>

<label>
	<input type=checkbox bind:checked={yes}>
	Yes! Send me regular email spam
</label>

{#if yes}
	<p>Thank you. We will bombard your inbox and sell your personal details.</p>
{:else}
	<p>You must opt in to continue. If you're not paying, you're the product.</p>
{/if}

<button disabled={!yes}>
	Subscribe
</button>

<h2>Size</h2>

<label>
	<input type=radio bind:group={scoops} value={1}>
	One scoop
</label>

<label>
	<input type=radio bind:group={scoops} value={2}>
	Two scoops
</label>

<label>
	<input type=radio bind:group={scoops} value={3}>
	Three scoops
</label>

<h2>Flavours</h2>

{#each menu as flavour}
	<label>
		<input type=checkbox bind:group={flavours} value={flavour}>
		{flavour}
	</label>
{/each}

{#if flavours.length === 0}
	<p>Please select at least one flavour</p>
{:else if flavours.length > scoops}
	<p>Can't order more flavours than scoops!</p>
{:else}
	<p>
		You ordered {scoops} {scoops === 1 ? 'scoop' : 'scoops'}
		of {join(flavours)}
	</p>
{/if}















<br><br><br><br><br><br><br><br><br>