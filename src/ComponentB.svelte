<script>
	const { a, b } = $props();

	let v = $state(0);
	export function reset() {
		v = 0;
	}
	export function funcB() {
		v = 0;
	}
</script>

<h2>Comp B</h2>

a: {a}, b:{b}

<p>Value B: {v}</p>
<button
	onclick={() => {
		v++;
	}}
>
	Increment
</button>
