<script>
	import { onMount } from 'svelte';

	const urlRoots = [
		'https://blocks.roadtolarissa.com/',
		'https://web.archive.org/web/20221201044944/https://bl.ocks.org/'
	];

	let urls = urlRoots;

	let input;
	onMount(() => input.focus());

	const blocksRoot = 'https://bl.ocks.org/';
	const gistRoot = 'https://gist.github.com/';

	const updateLinks = (e) => {
		const url = e.target.value.replace(blocksRoot, '').replace(gistRoot, '');
		urls = urlRoots.map((urlRoot) => urlRoot + url);
	};
</script>

<svelte:head><title>bl.ocks.org Mirror Links</title></svelte:head>

<div class="container">
	<h1><code>bl.ocks.org</code><br />Mirror Links</h1>

	<input
		type="text"
		placeholder="bl.ocks.org or gist URL"
		bind:this={input}
		on:input={updateLinks}
	/>

	<h2>Mirrors</h2>
	<ul>
		{#each urls as url}
			<li><a href={url} target="_blank" rel="noreferrer">{url}</a></li>
		{/each}
	</ul>

	<p>
		The official bl.ocks.org is currently down (more precisely, it redirects to GitHub Gists). This
		tool simplifies the process of finding your block of interest in another bl.ocks.org clone.
		Simply get the bl.ocks.org or gist link URL into the input field and open any of the generated
		links below it.
	</p>
</div>

<style>
	.container {
		padding: 45px;
		max-width: 1200px;
		margin-inline: auto;
	}

	h1,
	h2 {
		font-weight: 400;
	}

	code {
		letter-spacing: 0.06rem;
	}

	input {
		height: 2rem;
		width: min(35rem, 100%);
		margin: 1rem 0;
		padding: 0.2rem 0.5rem;
		border-radius: 0.2rem;
	}

	p {
		margin-top: 1.5rem;
	}

	li {
		list-style-type: circle;
		margin: 0.25rem 0;
	}
</style>
