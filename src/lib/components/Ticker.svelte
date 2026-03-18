<div class="ticker">
	<div class="tk-pill"><span class="tk-dot"></span>Live</div>
	<div class="tk-wrap">
		<span class="tk-track">
			{#each [0, 1] as _}
				&nbsp;&nbsp;<span class="tk-hi">SHIPGOALS</span><span class="tk-sep">·</span>EVENTS<span class="tk-sep">·</span>AUCTIONS<span class="tk-sep">·</span><span class="tk-hi">AND SO MUCH MORE TO COME</span><span class="tk-sep">·</span>SHIP TO KEEP IT ALIVE<span class="tk-sep">·</span><span class="tk-hi">EARN TOKENS</span><span class="tk-sep">·</span>LIVE ON HACKCLUB.TV<span class="tk-sep">·</span><span class="tk-hi">SHIPGOALS</span><span class="tk-sep">·</span>EVENTS<span class="tk-sep">·</span>AUCTIONS<span class="tk-sep">·</span><span class="tk-hi">AND SO MUCH MORE TO COME</span><span class="tk-sep">·</span>SHIP TO KEEP IT ALIVE<span class="tk-sep">·</span><span class="tk-hi">EARN TOKENS</span><span class="tk-sep">·</span>LIVE ON HACKCLUB.TV<span class="tk-sep">·</span>&nbsp;&nbsp;
			{/each}
		</span>
	</div>
</div>

<style>
	.ticker {
		background: #110808;
		height: 44px;
		width: 100%;
		display: flex;
		align-items: center;
		position: fixed;
		top: 0;
		left: 0;
		overflow: hidden;
		z-index: 10;
	}

	.ticker::before,
	.ticker::after {
		content: '';
		position: absolute;
		top: 0;
		bottom: 0;
		width: 80px;
		z-index: 2;
		pointer-events: none;
	}

	.ticker::before {
		left: 0;
		background: linear-gradient(90deg, #110808, transparent);
	}

	.ticker::after {
		right: 0;
		background: linear-gradient(-90deg, #110808, transparent);
	}

	.tk-pill {
		position: absolute;
		left: 16px;
		z-index: 3;
		display: flex;
		align-items: center;
		gap: 6px;
		background: #c0392b;
		border-radius: 999px;
		padding: 3px 10px 3px 7px;
		font-family: 'Phantom Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
		font-size: 10px;
		font-weight: 700;
		letter-spacing: 0.1em;
		color: #fff;
		text-transform: uppercase;
		white-space: nowrap;
	}

	.tk-dot {
		width: 6px;
		height: 6px;
		background: #fff;
		border-radius: 50%;
		animation: blink 1.2s ease-in-out infinite;
	}

	@keyframes blink {
		0%,
		100% {
			opacity: 1;
		}
		50% {
			opacity: 0.3;
		}
	}

	.tk-wrap {
		width: 100%;
		overflow: hidden;
		white-space: nowrap;
		padding-left: 100px;
	}

	.tk-track {
		display: inline-block;
		animation: scroll 10s linear infinite;
		font-family: 'Phantom Sans', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
		font-size: 11px;
		font-weight: 700;
		letter-spacing: 0.18em;
		color: rgba(255, 255, 255, 0.35);
		text-transform: uppercase;
	}

	.tk-hi {
		color: #e57373;
	}

	.tk-sep {
		color: rgba(255, 255, 255, 0.12);
		margin: 0 6px;
	}

	@keyframes scroll {
		from {
			transform: translateX(0);
		}
		to {
			transform: translateX(-50%);
		}
	}
</style>
