<script>
	import { fade, fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import { inview } from 'svelte-inview';

	// Define the 6 "Future Moments"
	const futureMoments = [
		{
			title: 'A Spring Picnic',
			description:
				'A relaxing picnic no parque da cidade, enjoy the spring weather and the lake scenery',
			icon: '🌸'
		},
		{
			title: 'Douro Weekend',
			description:
				'A perfect weekend where we go to the Douro river and enjoy the weekend wine tasting and sleeping in a suite',
			icon: '🍷'
		},
		{
			title: 'Dancing',
			description: 'Dancing with you in the room, living room, parties, social gatherings',
			icon: '💃'
		},
		{
			title: 'A Lazy Sunday',
			description: 'No alarms. Just us, in our future house enjoying each other',
			icon: '☀️'
		},
		{
			title: 'Travelling',
			description:
				"Sitting down, laptop on, picking the destination, planning and boom—we're there living the moment",
			icon: '✈️'
		},
		{
			title: 'Building a Family',
			description: 'Having beautiful children together, raising them, and giving them everything',
			icon: '👨‍👩‍👧‍👦'
		}
	];

	let heroVisible = false;
	let introVisible = false;
	let cardsVisible = {};

	// Initialize cards visibility state
	futureMoments.forEach((_, i) => {
		cardsVisible[i] = false;
	});

	function handleHeroChange({ detail }) {
		if (detail.inView) {
			heroVisible = true;
		}
	}

	function handleIntroChange({ detail }) {
		if (detail.inView) {
			introVisible = true;
		}
	}

	function handleCardChange(index, { detail }) {
		if (detail.inView) {
			cardsVisible[index] = true;
		}
	}
</script>

<div class="min-h-screen bg-[#FFFBEB] text-[#5C4033] font-sans antialiased">
	<section
		class="h-screen w-full flex flex-col items-center justify-center text-center p-4 relative overflow-hidden"
		use:inview
		on:inview_change={handleHeroChange}
	>
		<!-- Decorative hearts -->
		<svg
			class="absolute -top-12 -left-12 w-48 h-48 text-[#FFD100] opacity-30 transform -rotate-12 animate-pulse"
			xmlns="http://www.w3.org/2000/svg"
			viewBox="0 0 24 24"
			fill="currentColor"
		>
			<path
				d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"
			/>
		</svg>

		<svg
			class="absolute -bottom-12 -right-12 w-48 h-48 text-[#6A994E] opacity-20 transform rotate-12 animate-pulse"
			style="animation-delay: 1s;"
			xmlns="http://www.w3.org/2000/svg"
			viewBox="0 0 24 24"
			fill="currentColor"
		>
			<path
				d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"
			/>
		</svg>

		{#if heroVisible}
			<div class="relative z-10" in:fade={{ duration: 1000 }}>
				<h1 class="text-5xl md:text-7xl lg:text-8xl font-bold text-[#5C4033]">
					To Our Next 6 Months...
				</h1>
				<p class="text-xl md:text-2xl text-[#6A994E] mt-4 font-medium">
					...and all the adventures in between.
				</p>
			</div>
		{/if}
	</section>

	<section class="py-24" use:inview on:inview_change={handleIntroChange}>
		<div class="container mx-auto px-6 max-w-3xl text-center">
			{#if introVisible}
				<h2
					class="text-3xl md:text-4xl font-bold text-[#5C4033] mb-6"
					in:fly={{ y: 30, duration: 1000, easing: quintOut }}
				>
					Happy Half-Year, My Love
				</h2>
				<p
					class="text-lg md:text-xl leading-relaxed text-[#5C4033]/90"
					in:fly={{ y: 30, duration: 1000, delay: 400, easing: quintOut }}
				>
					Today marks 6 months of us being together, 6 months of nothing but happiness, moments, and
					experiences together. I wanted to celebrate us not by looking back, but by dreaming
					forward. So I organized below six moments I wish to share with you. Here's to a future
					filled with even more laughter, support, and love.
				</p>
			{/if}
		</div>
	</section>

	<section class="py-24">
		<div class="container mx-auto px-6 max-w-5xl">
			<h2 class="text-3xl md:text-4xl font-bold text-center text-[#5C4033] mb-16">
				6 Future Moments With You
			</h2>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-8 lg:gap-12">
				{#each futureMoments as moment, i}
					<div
						use:inview={{ unobserveOnEnter: true, rootMargin: '-100px' }}
						on:inview_change={(e) => handleCardChange(i, e)}
					>
						{#if cardsVisible[i]}
							<div
								in:fly={{ y: 50, duration: 1000, delay: (i % 2) * 200, easing: quintOut }}
								class="card bg-white border-2 border-[#6A994E] shadow-lg rounded-lg overflow-hidden
                       transition-all duration-300 ease-in-out transform
                       hover:scale-[1.03] hover:shadow-2xl hover:border-[#FFD100]"
							>
								<header
									class="p-6 border-b-4 border-[#FFD100] bg-gradient-to-br from-[#FFFBEB] to-white"
								>
									<div class="flex items-center gap-3">
										<span class="text-4xl">{moment.icon}</span>
										<h3 class="text-2xl font-bold text-[#5C4033]">{moment.title}</h3>
									</div>
								</header>

								<div class="p-6">
									<p class="text-[#5C4033]/90 leading-relaxed">{moment.description}</p>
								</div>
							</div>
						{/if}
					</div>
				{/each}
			</div>
		</div>
	</section>

	<footer class="text-center py-16 text-[#5C4033]/70">
		<p class="text-lg">With all my love, always. ❤️</p>
	</footer>
</div>

<style>
	@keyframes pulse {
		0%,
		100% {
			opacity: 0.3;
		}
		50% {
			opacity: 0.5;
		}
	}

	.animate-pulse {
		animation: pulse 3s ease-in-out infinite;
	}
</style>
