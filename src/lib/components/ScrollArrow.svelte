<!-- Scroll Down Arrow -->
<div class="scroll-down-container">
	<a
		href="#links"
		class="scroll-down-arrow"
		on:click|preventDefault={() => {
			// Scroll the window to the scroll container section
			window.scrollTo({
				top: window.innerHeight,
				behavior: 'smooth'
			});
		}}
	>
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
			<path d="M12 20L12 4M12 20L6 14M12 20L18 14" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
		</svg>
		<div class="scroll-arrow-background"></div>
	</a>
</div>

<style>
	.scroll-down-container {
		position: absolute;
		bottom: 2rem;
		left: 50%;
		transform: translateX(-50%);
		z-index: 30;
		cursor: pointer;
	}

	.scroll-down-arrow {
		display: block;
		color: white;
		transition: transform 0.3s ease;
		position: relative;
	}

	.scroll-down-arrow svg {
		width: 3rem;
		height: 3.5rem;
		filter: drop-shadow(0 0 8px rgba(255, 255, 255, 0.6));
		transition: all 0.3s ease;
	}

	.scroll-down-arrow:hover svg {
		transform: translateY(4px);
		filter: drop-shadow(0 0 12px rgba(255, 255, 255, 0.9));
	}

	.scroll-arrow-background {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 3rem;
		height: 3rem;
		background: rgba(255, 255, 255, 0.1);
		border-radius: 50%;
		backdrop-filter: blur(10px);
		z-index: -1;
	}

	/* Mobile styles */
	@media (max-width: 768px) {
		.scroll-down-container {
			position: absolute;
			bottom: 1.5rem;
			left: 50%;
			transform: translateX(-50%);
			z-index: 30;
		}

		.scroll-down-arrow svg {
			width: 3.5rem;
			height: 4rem;
			filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.8));
		}

		.scroll-down-arrow:hover svg {
			transform: translateY(6px);
			filter: drop-shadow(0 0 15px rgba(255, 255, 255, 1));
		}
	}
</style>