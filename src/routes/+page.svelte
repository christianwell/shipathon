<script lang="ts">
	import Ticker from '$lib/components/Ticker.svelte';
	import { track } from '@vercel/analytics';
	import { onMount } from 'svelte';

	let visible = $state(false);

	let faqVisible = $state(false);
	let openIndex = $state(-1);

	const faqs = [
		{
			q: 'You ship, We stream?',
			a: "Yeah you heard that right YOU ship and WE STREAM ON <a href=\"https://hackclub.tv\" target=\"_blank\" rel=\"noopener noreferrer\">HACKCLUB.TV</a> "
		},
		{
			q: "What even is a shipathon?",
			a: "You heard of a subathon, and a shipathon is hack club's spin on that! ship hours keep the stream <span class=\"alive\">alive</span>"
		},
		{
			q: "But what do I get?",
			a: "We will have a shop where users can buy items with the hours they ship, and were gonna run events like live auctions."
		},
		{
			q: "What's gonna happen on the stream?",
			a: "EVENTS, AUCTIONS AND SO MUCH MORE TO COME"
		},
		{
			q: "When does this end?",
			a: "YOU PICK THE END. When the stream runs out of time, the shipathon is over. Keep shipping to keep it <span class=\"alive\">alive</span>."
		}
	];

	function toggle(i: number) {
		openIndex = openIndex === i ? -1 : i;
	}

	onMount(() => {
		visible = true;

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (!entry.isIntersecting) return;
						if (entry.target.classList.contains('faq')) faqVisible = true;
				});
			},
			{ threshold: 0.15 }
		);

		const el = document.querySelector('.faq');
		if (el) observer.observe(el);

		return () => observer.disconnect();
	});
</script>

<Ticker />

<div class="page">


	<main class:visible>
		<p class="hero-eyebrow">Hack Club presents</p>
		<h1 class="logo">shipathon</h1>
		<p class="tagline">You ship. <span class="alive">We stream.</span></p>
		<p class="hero-desc">You heard of a subathon, well this is Hack Club's spin on it.<br />Ship hours, earn tokens, and keep a 24/7 live stream of HQ basement <span class="alive">alive</span> on <a href="https://hackclub.tv" target="_blank" rel="noopener noreferrer">hackclub.tv</a></p>
		<a href="https://forms.fillout.com/t/fXkrkbBBShus" target="_blank" rel="noopener noreferrer" class="rsvp-btn" onclick={() => track('rsvp_click')}>RSVP</a>
		<a href="#faq" class="scroll-arrow" aria-label="Scroll to FAQ">
			<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 12 15 18 9"></polyline></svg>
		</a>
	</main>
	<span class="photo-credit">photo credit — lynn</span>
	<footer class="hero-footer">
		<div class="footer-center">
			<p class="made">Made with ❤️ by Hack Club!</p>
			<p><a href="https://github.com/christianwell/shipathon" target="_blank" rel="noopener">All code is open sourced here!</a></p>
			<p class="legal">Hack Club. 501(c)(3) nonprofit (EIN: 81-2908499)</p>
		</div>
	</footer>
</div>



<section id="faq" class="faq" class:faqVisible>
	<div class="faq-inner">
		<div class="faq-left">
			<h2 class="faq-heading">
				<span>You ship.</span>
				<span class="red">We stream.</span>
			</h2>
		</div>

		<div class="faq-right">
			{#each faqs as faq, i}
				<button
					class="faq-item"
					class:open={openIndex === i}
					style="--i: {i}"
					onclick={() => toggle(i)}
				>
					<div class="faq-q">
						<span class="faq-q-text">{faq.q}</span>
						<span class="faq-toggle">{openIndex === i ? '−' : '+'}</span>
					</div>
					<div class="faq-a">
						<p>{@html faq.a}</p>
					</div>
				</button>
			{/each}
		</div>
	</div>
</section>

<style>
	:global(*) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	:global(html, body) {
		height: 100%;
		overflow-x: hidden;
		background: #000;
		color: #fff;
		font-family: 'Phantom Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
	}

	.page {
		position: relative;
		width: 100%;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		background: linear-gradient(rgba(0, 0, 0, 0.6), rgba(0, 0, 0, 0.75)),
			url('/basement.webp');
		background-size: cover;
		background-position: center;
		background-repeat: no-repeat;
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
	}

	.tagline {
		font-family: 'Phantom Sans', system-ui, sans-serif;
		font-style: italic;
		font-size: clamp(1rem, 3vw, 1.8rem);
		color: rgba(255, 255, 255, 0.9);
		margin-top: 1rem;
		text-shadow: 0 2px 12px rgba(0, 0, 0, 0.9);
	}

	.alive,
	:global(.alive) {
		color: #ec3750;
		font-style: italic;
	}

	.hero-eyebrow {
		font-size: 0.8rem;
		font-weight: 700;
		letter-spacing: 0.2em;
		text-transform: uppercase;
		color: #ec3750;
	}

	.hero-desc {
		font-size: clamp(0.95rem, 2vw, 1.15rem);
		color: rgba(255, 255, 255, 0.5);
		line-height: 1.7;
		margin-top: 1.25rem;
		max-width: 540px;
	}

	.hero-desc a {
		color: #ec3750;
		text-decoration: underline;
	}

	.rsvp-btn {
		display: inline-block;
		margin-top: 1.75rem;
		padding: 0.85rem 2.5rem;
		background: #ec3750;
		color: #fff;
		font-family: 'Phantom Sans', system-ui, sans-serif;
		font-size: 1.1rem;
		font-weight: 700;
		letter-spacing: 0.08em;
		text-transform: uppercase;
		text-decoration: none;
		border-radius: 8px;
		box-shadow: 0 0 20px rgba(236, 55, 80, 0.4), 0 4px 12px rgba(0, 0, 0, 0.3);
		transition: background 0.2s ease, transform 0.15s ease, box-shadow 0.2s ease;
	}

	.rsvp-btn:hover {
		background: #d42f45;
		transform: translateY(-3px);
		box-shadow: 0 0 30px rgba(236, 55, 80, 0.6), 0 6px 20px rgba(0, 0, 0, 0.4);
	}

	.rsvp-btn:active {
		transform: translateY(0);
		box-shadow: 0 0 15px rgba(236, 55, 80, 0.3), 0 2px 8px rgba(0, 0, 0, 0.3);
	}

	.scroll-arrow {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		margin-top: 2rem;
		color: rgba(255, 255, 255, 0.4);
		animation: bounce 2s ease-in-out infinite;
		text-decoration: none;
	}

	.scroll-arrow:hover {
		color: #ec3750;
	}

	@keyframes bounce {
		0%, 100% { transform: translateY(0); }
		50% { transform: translateY(8px); }
	}

	.photo-credit {
		position: absolute;
		left: 1rem;
		bottom: 4.5rem;
		font-size: 11px;
		color: rgba(255, 255, 255, 0.25);
		z-index: 2;
		letter-spacing: 0.05em;
	}

	.hero-footer {
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

	.faq {
		background: #000;
		padding: 6rem 2rem;
	}

	.faq-inner {
		max-width: 960px;
		margin: 0 auto;
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 4rem;
		align-items: start;
	}

	.faq-left {
		position: sticky;
		top: 6rem;
		opacity: 0;
		transform: translateY(24px);
		transition: opacity 0.6s ease, transform 0.6s ease;
	}

	.faqVisible .faq-left {
		opacity: 1;
		transform: none;
	}

	.faq-heading {
		font-size: clamp(2.4rem, 5vw, 3.6rem);
		font-weight: 900;
		line-height: 1.1;
		letter-spacing: -0.02em;
		margin: 0;
	}

	.faq-heading span {
		display: block;
	}

	.faq-heading .red {
		color: #ec3750;
	}

	.faq-right {
		display: flex;
		flex-direction: column;
	}

	.faq-item {
		all: unset;
		display: block;
		cursor: pointer;
		width: 100%;
		border-top: 1px solid rgba(255, 255, 255, 0.1);
		opacity: 0;
		transform: translateY(12px);
		transition: opacity 0.4s ease calc(var(--i) * 0.07s),
			transform 0.4s ease calc(var(--i) * 0.07s);
	}

	.faq-item:last-child {
		border-bottom: 1px solid rgba(255, 255, 255, 0.1);
	}

	.faqVisible .faq-item {
		opacity: 1;
		transform: none;
	}

	.faq-q {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 1.25rem 0;
		gap: 1rem;
	}

	.faq-q-text {
		font-size: clamp(0.95rem, 2vw, 1.1rem);
		font-weight: 600;
		color: rgba(255, 255, 255, 0.8);
		text-align: left;
	}

	.faq-toggle {
		font-size: 1.25rem;
		font-weight: 300;
		color: rgba(255, 255, 255, 0.3);
		flex-shrink: 0;
		width: 24px;
		text-align: center;
		transition: color 0.2s ease;
	}

	.faq-item:hover .faq-q-text {
		color: #fff;
	}

	.faq-item:hover .faq-toggle {
		color: rgba(255, 255, 255, 0.6);
	}

	.faq-item.open .faq-toggle {
		color: #ec3750;
	}

	.faq-a {
		display: grid;
		grid-template-rows: 0fr;
		transition: grid-template-rows 0.3s ease;
	}

	.faq-item.open .faq-a {
		grid-template-rows: 1fr;
	}

	.faq-a p {
		overflow: hidden;
		font-size: 0.95rem;
		color: rgba(255, 255, 255, 0.4);
		line-height: 1.65;
		padding-bottom: 0;
		transition: padding-bottom 0.3s ease;
	}

	.faq-item.open .faq-a p {
		padding-bottom: 1.25rem;
	}

	.faq-a :global(a) {
		color: #ec3750;
		text-decoration: underline;
	}

	@media (max-width: 700px) {
		.faq-inner {
			grid-template-columns: 1fr;
			gap: 2.5rem;
		}

		.faq-left {
			position: static;
			text-align: center;
		}

		.faq-heading {
			font-size: 2.2rem;
		}
	}
</style>
