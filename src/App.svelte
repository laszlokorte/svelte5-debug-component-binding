<script>
	import ComponentA from './ComponentA.svelte';
	import ComponentB from './ComponentB.svelte';
	import ComponentC from './ComponentC.svelte';
	import ComponentD from './ComponentD.svelte';

	const components = {
		a: {
			svelte: ComponentA,
			params: { x: 3, y: 2 }
		},
		b: {
			svelte: ComponentB,
			params: { a: 3, b: 2 }
		},
		c: {
			svelte: ComponentC,
			params: { a: 3, b: 2 }
		},
		d: {
			svelte: ComponentD,
			params: { a: 3, b: 2 }
		}
	};

	const parameters = {
		x: 5,
		y: 3
	};

	let comp = $state('c');
	let currentInstanceRaw = $state.frozen({ value: undefined });

	const currentInstance = {
		get value() {
			return currentInstanceRaw.value;
		},
		set value(v) {
			console.log(v);
			currentInstanceRaw = {
				value: v
			};
		}
	};
</script>

<select bind:value={comp}>
	{#each Object.keys(components) as c}
		<option value={c}>{c}</option>
	{/each}
</select>

<button
	onclick={() => {
		if (currentInstance.value === null) {
			throw new Error('Component binding is null but should not');
		}
		if (currentInstance.value.reset) {
			currentInstance.value.reset();
		}
	}}>Reset current Component</button
>

<hr />

<svelte:component
	this={components[comp].svelte}
	bind:this={currentInstance.value}
	key={comp}
	{...components[comp].params}
/>
