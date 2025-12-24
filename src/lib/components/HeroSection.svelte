<!-- Floating Text Overlay -->
<div
	id="kawaii-text-overlay"
	class="pointer-events-none absolute top-0 left-0 z-10 flex h-screen w-full select-none items-center justify-center p-4"
>
	<h1
		class="font-kawaii text-center text-5xl font-extrabold text-white drop-shadow-kawaii sm:text-6xl md:text-7xl lg:text-8xl"
	>
		CatCafe
		<span class="sparkle-divider mx-1 inline-block text-4xl sm:text-5xl md:text-6xl lg:text-7xl">✨</span>
		Space
		<span style="font-size: 0.5em; vertical-align: super; opacity: 0.9; color: #FFDAB9; margin-left: -0.1em;">:3</span>
	</h1>
</div>

<style>
	.font-kawaii {
		font-family: 'Pacifico', cursive;
	}

	.drop-shadow-kawaii {
		filter:
			drop-shadow(0 0 4px rgba(255, 182, 193, 0.8)) /* Pink */
			drop-shadow(0 0 10px rgba(173, 216, 230, 0.7)) /* Blue */
			drop-shadow(0 0 18px rgba(255, 218, 185, 0.6)) /* Peach */
			drop-shadow(0 0 30px rgba(221, 160, 221, 0.5)); /* Plum */
	}

	.sparkle-divider {
		filter: drop-shadow(0 0 5px gold);
		animation: sparkle-pulse 2s infinite ease-in-out;
		transform-origin: center;
	}

	@keyframes sparkle-pulse {
		0%, 100% { transform: scale(1); opacity: 0.9; }
		50% { transform: scale(1.15); opacity: 1; }
	}
</style>