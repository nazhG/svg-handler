<script>
    import svgs from './svg.js';
	import { onMount } from 'svelte';

	onMount(() => {
		console.table(svgs);
		for (let index = 0; index < 3; index++) {
			let a = document.getElementById(index);
			let svg = a.nextElementSibling;
			const base64doc = btoa(unescape(encodeURIComponent(svg.outerHTML)));
			// const e = new MouseEvent('click');
			a.download = 'file.svg';
			// a.href = 'data:image/svg+xml;base64,' + base64doc;
			// a.dispatchEvent(e);
			a.setAttribute('href', 'data:image/svg+xml;base64,' + base64doc);
		}
	});

	function handlerDownload(i) {
		window.document.getElementById(i).nextElementSibling.outerHTML
	}
</script>

<main>
	{#each Array(3) as x, i}
		<a id="{i}" href="./" on:click={handlerDownload(i)}> Download</a>
		<svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="dog" class="svg-inline--fa fa-dog fa-w-18" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512">
			<path fill="blue" d={svgs.things[1]}></path>
			<path fill="red" transform='translate(90 150) scale(0.4)' d={svgs.animals[i]}></path>
		</svg>
	{/each}
</main>

<style>
	svg {
		width: 120px;
		padding: 10px;
	}

	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>