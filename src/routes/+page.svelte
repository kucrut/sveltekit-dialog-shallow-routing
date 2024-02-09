<script>
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';

	import { page } from '$app/stores';
	import { pushState } from '$app/navigation';
	import Dialog from '$lib/components/dialog.svelte';

	function open_dialog() {
		pushState( '', {
			show_modal: true,
		} );
	}

	function close_dialog() {
		history.back();
	}
</script>

<svelte:head>
	<title>Dialog with Shallow Routing</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		<span class="welcome">
			<picture>
				<source srcset={welcome} type="image/webp" />
				<img src={welcome_fallback} alt="Welcome" />
			</picture>
		</span>
	</h1>

	<div>
		<p>This page demonstrates how to use native <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog">HTML Dialog</a> element along with the <a href="https://kit.svelte.dev/docs/shallow-routing">shallow routing</a> feature in SvelteKit. When the dialog is open, clicking on the close button or the backdrop, or hitting the browser back button will close it.</p>


		<button on:click={open_dialog}>Open Dialog</button>
	</div>

	<div>
		<a href="https://github.com/kucrut/sveltekit-dialog-shallow-routing">Fork on GitHub</a>
	<div>

	{#if $page.state.show_modal}
		<Dialog on:close={close_dialog}>
			<p>Hello, and welcome!</p>
			<button on:click={close_dialog}>Close</button>
		</Dialog>
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}

	div {
		margin-block: 2rem;
		text-align: center;
	}
</style>
