<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	const items = [
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/>`,
			title: 'Modern technológia',
			desc: 'Ipari kategóriájú lézertisztító berendezések.',
			color: 'orange',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>`,
			title: 'Környezetbarát',
			desc: 'Vegyszermentes, minimális hulladék, fenntartható megoldás.',
			color: 'blue',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>`,
			title: 'Helyi szolgáltató',
			desc: 'Baranya megye és Dél-Dunántúl – közel vagyunk, gyorsan érünk oda.',
			color: 'orange',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"/>`,
			title: 'Rugalmas időpontok',
			desc: 'Az Ön igényeihez igazodó munkaidő és helyszín.',
			color: 'blue',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M13 10V3L4 14h7v7l9-11h-7z"/>`,
			title: 'Gyors reakcióidő',
			desc: 'Ajánlatkérés után rövid időn belül visszajelzünk.',
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

<section id="bizalom" class="py-24 lg:py-32 bg-[#0c0c0c] relative overflow-hidden" bind:this={section}>
	<!-- Accent -->
	<div class="absolute inset-0 pointer-events-none" style="
		background: radial-gradient(ellipse 80% 40% at 50% 50%, rgba(249,115,22,0.04) 0%, transparent 70%);
	"></div>

	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
		<div class="text-center mb-16 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Miért minket válasszon?</h2>
		</div>

		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-5">
			{#each items as item, i}
				<div
					class="card fade-in text-center flex flex-col items-center"
					style="transition-delay: {i * 0.08}s;"
				>
					<div
						class="w-14 h-14 rounded-2xl mb-4 flex items-center justify-center"
						style="background: {item.color === 'orange' ? 'rgba(249,115,22,0.12)' : 'rgba(59,130,246,0.12)'};"
					>
						<svg
							class="w-7 h-7"
							style="color: {item.color === 'orange' ? '#f97316' : '#3b82f6'};"
							fill="none" viewBox="0 0 24 24" stroke="currentColor"
						>
							{@html item.icon}
						</svg>
					</div>
					<h3 class="text-white font-bold mb-2 text-sm">{item.title}</h3>
					<p class="text-gray-500 text-xs leading-relaxed">{item.desc}</p>
				</div>
			{/each}
		</div>

		<!-- Final CTA banner -->
		<div class="mt-16 fade-in">
			<div class="relative rounded-2xl overflow-hidden border border-orange-500/20 bg-gradient-to-r from-orange-500/10 via-[#1a1a1a] to-blue-500/10 px-8 py-10 text-center">
				<h3 class="text-2xl lg:text-3xl font-bold text-white mb-3">
					Kérjen ajánlatot most!
				</h3>
				<p class="text-gray-400 mb-6 max-w-xl mx-auto">
					Küldjön fotót vagy rövid leírást, és rövid időn belül visszajelzünk.
				</p>
				<a href="#kapcsolat" class="btn-primary text-lg px-8 py-4">
					Ajánlatkérő űrlap
					<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"/>
					</svg>
				</a>
			</div>
		</div>
	</div>
</section>
