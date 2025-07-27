<!-- Vertical Scroll Container for Link Cards -->
<div class="scroll-container" id="links">
	<div class="scroll-content">
		<!-- Card 1: Cat-a-log -->
		<a
			href="https://log.catcafe.space"
			target="_blank"
			rel="noopener noreferrer"
			class="log-button group"
		>
			<img src="/cat-a-log.png" alt="Cat-a-log Logo" class="log-button-logo" />
			<div class="flex-1">
				<p class="log-button-title">Enter the Cat-a-log</p>
				<p class="log-button-description">
					Your cosmic logbook for every feline friend you meet. Chart your encounters across the
					galaxy and let the adventure begin! ✨
				</p>
			</div>
		</a>

		<!-- Card 2: Cat String -->
		<a
			href="https://string.catcafe.space"
			target="_blank"
			rel="noopener noreferrer"
			class="log-button group"
		>
			<img src="/yarn-16-svgrepo-com.svg" alt="Yarn Ball Icon" class="log-button-logo" />
			<div class="flex-1">
				<p class="log-button-title">Cat String Physics</p>
				<p class="log-button-description">
					An interactive physics-based string simulation! Watch realistic string dynamics as you play with virtual cat toys. Pounce, swat, and chase in this purr-fectly realistic playground! 🧶✨
				</p>
			</div>
		</a>
	</div>
</div>

<style>
	.scroll-container {
		width: 100%;
		z-index: 20;
		margin-top: 100vh; /* Position below the initial viewport */
		padding-bottom: 5rem;
		overflow-y: auto; /* Enable scrolling only in this container */
	}

	.scroll-content {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1.5rem; /* 24px */
		padding: 0 1rem;
	}

	.log-button {
		display: flex;
		align-items: center;
		gap: 1.5rem; /* 24px */
		padding: 1.5rem; /* 24px */
		background: rgba(255, 255, 255, 0.1);
		border: 1px solid rgba(255, 255, 255, 0.2);
		border-radius: 1rem; /* 16px */
		backdrop-filter: blur(10px);
		transition: all 0.4s ease;
		text-decoration: none;
		color: inherit;
		width: 100%;
		max-width: 32rem; /* 512px */
		box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
	}

	.log-button:hover {
		background: rgba(255, 255, 255, 0.15);
		border-color: rgba(255, 255, 255, 0.3);
		transform: translateY(-4px);
		box-shadow: 0 8px 30px rgba(0, 0, 0, 0.2);
	}

	.log-button-logo {
		width: 5rem; /* 80px */
		height: 5rem; /* 80px */
		flex-shrink: 0;
		filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.5));
		transition: transform 0.4s ease;
		color: white; /* For SVG stroke */
	}

	.group:hover .log-button-logo {
		transform: rotate(-10deg) scale(1.05);
	}

	.log-button-title {
		font-family: 'Pacifico', cursive;
		font-size: 1.75rem; /* 28px */
		line-height: 1.2;
		color: #f3a0e8; /* Light purple from gradient */
	}

	.log-button-description {
		margin-top: 0.5rem; /* 8px */
		font-size: 0.9rem; /* 14.4px */
		color: rgba(255, 255, 255, 0.85);
		line-height: 1.5;
	}
</style>