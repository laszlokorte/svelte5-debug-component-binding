<script>
	const { x, y } = $props();

	let v = $state(0);

	export function reset() {
		v = 0;
	}
	export function funcA() {
		v = 0;
	}
</script>

<h2>Comp A</h2>

x: {x}, y: {y}

<p>Value A: {v}</p>
<button
	onclick={() => {
		v++;
	}}
>
	Increment
</button>
