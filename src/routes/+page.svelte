<script lang="ts">
	import Ticker from '$lib/components/Ticker.svelte';
	import { onMount } from 'svelte';

	let visible = $state(false);

	onMount(() => {
		visible = true;
	});
</script>

<Ticker />

<div class="page">
	<div class="bg"></div>
	<div class="vignette"></div>

	<main class:visible>
		<h1 class="logo">shipathon</h1>
		<p class="tagline">ship projects, keep the stream <span class="alive">alive</span></p>
		<h2 class="coming-soon">COMING SOON</h2>
	</main>

	<footer>
		<span class="credits">CREDITS LYNN'S PHOTO</span>
		<div class="footer-center">
			<p class="made">Made with ❤️ by Hack Club!</p>
			<p><a href="https://github.com/hackclub" target="_blank" rel="noopener">All code is open sourced here!</a></p>
			<p class="legal">Hack Club. 501(c)(3) nonprofit (EIN: 81-2908499)</p>
		</div>
	</footer>
</div>

<style>
	:global(*) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	:global(html, body) {
		height: 100%;
		overflow: hidden;
		background: #000;
		color: #fff;
		font-family: 'Phantom Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
	}

	.page {
		position: relative;
		width: 100%;
		height: 100vh;
		display: flex;
		flex-direction: column;
	}

	.bg {
		position: absolute;
		inset: 0;
		background: url('https://cdn.hackclub.com/019cef53-06a8-7027-bbfe-a13878ec397a/shipathon__1_.png')
			center / cover no-repeat;
		z-index: 0;
	}

	.vignette {
		position: absolute;
		inset: 0;
		background:
			linear-gradient(to bottom, rgba(0, 0, 0, 0.4) 0%, transparent 15%),
			linear-gradient(to top, rgba(0, 0, 0, 0.6) 0%, transparent 25%),
			radial-gradient(ellipse at center, transparent 40%, rgba(0, 0, 0, 0.5) 100%);
		z-index: 1;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		z-index: 2;
		padding-top: 44px;
		text-align: center;
		padding-left: 1rem;
		padding-right: 1rem;
	}

	.logo {
		font-family: 'Phantom Sans', system-ui, sans-serif;
		font-size: clamp(3.5rem, 10vw, 7rem);
		font-weight: bold;
		color: #fff;
		text-shadow:
			0 4px 30px rgba(0, 0, 0, 0.9),
			0 2px 10px rgba(0, 0, 0, 0.7);
		line-height: 0.9;
		letter-spacing: -0.02em;
		opacity: 0;
		transform: translateY(20px);
		transition: opacity 0.8s ease, transform 0.8s ease;
	}

	.tagline {
		font-family: 'Phantom Sans', system-ui, sans-serif;
		font-style: italic;
		font-size: clamp(1rem, 3vw, 1.8rem);
		color: rgba(255, 255, 255, 0.9);
		margin-top: 1rem;
		text-shadow: 0 2px 12px rgba(0, 0, 0, 0.9);
		opacity: 0;
		transform: translateY(20px);
		transition: opacity 0.8s ease 0.2s, transform 0.8s ease 0.2s;
	}

	.alive {
		color: #ec3750;
		font-style: italic;
	}

	.coming-soon {
		font-family: 'Phantom Sans', system-ui, sans-serif;
		font-size: clamp(1.6rem, 4vw, 2.8rem);
		font-weight: bold;
		font-style: italic;
		text-transform: uppercase;
		margin-top: 1.5rem;
		letter-spacing: 0.05em;
		text-shadow:
			0 4px 20px rgba(0, 0, 0, 0.9),
			0 2px 8px rgba(0, 0, 0, 0.7);
		opacity: 0;
		transform: translateY(20px);
		transition: opacity 0.8s ease 0.4s, transform 0.8s ease 0.4s;
	}

	main.visible .logo,
	main.visible .tagline,
	main.visible .coming-soon {
		opacity: 1;
		transform: translateY(0);
	}

	footer {
		position: relative;
		z-index: 2;
		padding: 1.25rem 2rem 1.5rem;
		display: flex;
		align-items: flex-end;
		justify-content: center;
	}

	.credits {
		position: absolute;
		left: 1.5rem;
		bottom: 1.5rem;
		font-family: 'Courier New', monospace;
		font-size: 11px;
		letter-spacing: 0.15em;
		color: rgba(255, 255, 255, 0.25);
		text-transform: uppercase;
	}

	.footer-center {
		text-align: center;
		font-family: 'Phantom Sans', system-ui, sans-serif;
		font-size: 14px;
		color: rgba(255, 255, 255, 0.6);
		line-height: 1.5;
	}

	.made {
		font-weight: bold;
		color: rgba(255, 255, 255, 0.8);
	}

	.footer-center a {
		color: rgba(255, 255, 255, 0.6);
		text-decoration: underline;
		text-underline-offset: 2px;
	}

	.footer-center a:hover {
		color: #fff;
	}

	.legal {
		font-size: 12px;
		color: rgba(255, 255, 255, 0.35);
	}

	@media (max-width: 600px) {
		.credits {
			display: none;
		}
	}
</style>
