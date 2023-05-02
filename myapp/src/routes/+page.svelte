<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>

<script>
	export let foo;
    foo = 1515;

	// プロパティとして渡された変数は、
	// 即座に使用可能になります
	console.log({ foo });
</script>