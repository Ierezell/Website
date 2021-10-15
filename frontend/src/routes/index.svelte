<script lang="ts">
	import { uniqueNamesGenerator, names } from 'unique-names-generator';
	import Hello from '../components/Hello.svelte';
	const name = uniqueNamesGenerator({ dictionaries: [names, names], separator: ' ', length: 2 });
	const manyNames = Array.from({ length: 10 }, () =>
		uniqueNamesGenerator({ dictionaries: [names, names], separator: ' ', length: 2 })
	);

	let count = 0;
	let numbers = [1, 2, 3, 4];
	$: doubled = count * 2;

	function incrementCount() {
		count += 1;
	}

	function addNumber() {
		numbers = [...numbers, numbers.length + 1];
	}

	$: sum = numbers.reduce((t, n) => t + n, 0);
</script>

<div>
	<h1>Hello {name}</h1>
	<h3>Welcome to The Website</h3>
	<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
	<Hello {name} />
	{#if count < 9}
		<button on:click={incrementCount}>
			Clicked {count}
			{count === 1 ? 'time' : 'times'} and times two it's {doubled}
		</button>
	{:else}
		<h1>THAT'S ENOUGH</h1>
	{/if}
	<p>{numbers.join(' + ')} = {sum}</p>
	<button on:click={addNumber}> Add a number </button>
	<h4>Thanks to</h4>
	<ul>
		{#each manyNames as n, i}
			<li>
				{i + 1}
				{n}
			</li>
		{/each}
	</ul>
</div>

<style>
	p {
		text-align: center;
		color: purple;
		font-size: 2em;
	}

	h1 {
		color: blue;
		text-align: center;
	}
	div {
		display: grid;
		justify-content: center;
		align-items: center;
	}
</style>
