<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	const steps = [
		{
			num: '01',
			title: 'Kapcsolatfelvétel',
			desc: 'Vegye fel velünk a kapcsolatot telefonon, e-mailen vagy küldjön fotót a felületről.',
			color: 'orange',
		},
		{
			num: '02',
			title: 'Előzetes árajánlat',
			desc: 'A fotók vagy leírás alapján rövid időn belül tájékoztató árajánlatot küldünk.',
			color: 'blue',
		},
		{
			num: '03',
			title: 'Időpont egyeztetés',
			desc: 'Rugalmas időpontban egyeztetünk a helyszíni munkavégzésre.',
			color: 'orange',
		},
		{
			num: '04',
			title: 'Helyszíni tisztítás',
			desc: 'Szakképzett munkatársunk elvégzi a lézeres tisztítást az Ön telephelyén.',
			color: 'blue',
		},
		{
			num: '05',
			title: 'Azonnali eredmény',
			desc: 'A munka végeztével azonnal látja az eredményt – tiszta felület, kompromisszumok nélkül.',
			color: 'orange',
		},
	];

	onMount(() => {
		const obs = new IntersectionObserver(
			(entries) => entries.forEach(e => e.target.classList.toggle('visible', e.isIntersecting)),
			{ threshold: 0.1 }
		);
		section.querySelectorAll('.fade-in').forEach(el => obs.observe(el));
		return () => obs.disconnect();
	});
</script>

<section id="hogyan-dolgozunk" class="py-24 lg:py-32 bg-[#0c0c0c] relative" bind:this={section}>
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">

		<div class="text-center mb-16 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Hogyan dolgozunk?</h2>
			<p class="text-gray-500 max-w-xl mx-auto">Egyszerű, átlátható folyamat az első kapcsolatfelvételtől az eredményig</p>
		</div>

		<!-- Timeline -->
		<div class="relative">
			<!-- Connector line (desktop) -->
			<div class="hidden lg:block absolute top-10 left-0 right-0 h-px bg-gradient-to-r from-transparent via-[#2a2a2a] to-transparent"></div>

			<div class="grid grid-cols-1 lg:grid-cols-5 gap-8 lg:gap-4">
				{#each steps as step, i}
					<div class="fade-in flex flex-col items-center text-center" style="transition-delay: {i * 0.12}s;">
						<!-- Number circle -->
						<div
							class="relative z-10 w-20 h-20 rounded-full border-2 flex items-center justify-center mb-6 text-2xl font-black transition-transform hover:scale-110"
							style="
								background: #0f0f0f;
								border-color: {step.color === 'orange' ? '#f97316' : '#3b82f6'};
								color: {step.color === 'orange' ? '#f97316' : '#3b82f6'};
								box-shadow: 0 0 20px {step.color === 'orange' ? 'rgba(249,115,22,0.2)' : 'rgba(59,130,246,0.2)'};
							"
						>
							{step.num}
						</div>

						<h3 class="text-white font-bold mb-2">{step.title}</h3>
						<p class="text-gray-500 text-sm leading-relaxed">{step.desc}</p>

						<!-- Mobile connector -->
						{#if i < steps.length - 1}
							<div class="lg:hidden w-px h-8 mt-4 bg-gradient-to-b from-[#2a2a2a] to-transparent"></div>
						{/if}
					</div>
				{/each}
			</div>
		</div>

		<!-- CTA -->
		<div class="text-center mt-16 fade-in">
			<a href="#kapcsolat" class="btn-primary text-lg px-8 py-4">
				Indítsuk el!
				<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"/>
				</svg>
			</a>
		</div>
	</div>
</section>
