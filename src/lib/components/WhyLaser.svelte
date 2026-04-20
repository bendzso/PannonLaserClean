<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	const advantages = [
		{
			title: 'Nem károsítja az alapanyagot',
			desc: 'A lézer csak a szennyeződést távolítja el, az alatta lévő felület érintetlen marad.',
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"/>`,
		},
		{
			title: 'Vegyszermentes megoldás',
			desc: 'Nincs szükség agresszív tisztítószerekre vagy oldószerekre. Környezetbarát és biztonságos.',
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"/>`,
		},
		{
			title: 'Precíz és szabályozható',
			desc: 'A beállításokkal pontosan meghatározható a tisztítás intenzitása és mélysége.',
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"/>`,
		},
		{
			title: 'Nincs másodlagos hulladék',
			desc: 'Nem keletkezik homok, vegyszer vagy egyéb szennyező melléktermék – minimális utómunka.',
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"/>`,
		},
		{
			title: 'Gyors és hatékony',
			desc: 'Sok esetben jelentősen gyorsabb, mint a hagyományos módszerek. Azonnali eredmény.',
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M13 10V3L4 14h7v7l9-11h-7z"/>`,
		},
		{
			title: 'Mobil, helyszíni megoldás',
			desc: 'Nem kell szállítani az alkatrészeket – mi megyünk Önhöz, telephelyére vagy otthonába.',
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/>`,
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

<section id="miert-lezer" class="py-24 lg:py-32 relative" bind:this={section}>
	<!-- Background accent -->
	<div class="absolute inset-0 pointer-events-none" style="
		background: radial-gradient(ellipse 70% 50% at 50% 50%, rgba(59,130,246,0.04) 0%, transparent 70%);
	"></div>

	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative">
		<div class="text-center mb-16 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Miért lézeres tisztítás?</h2>
			<p class="text-gray-500 max-w-2xl mx-auto">
				A lézertechnológia előnyei más módszerekkel szemben
			</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
			{#each advantages as adv, i}
				<div class="fade-in relative group" style="transition-delay: {i * 0.1}s;">
					<div class="card h-full">
						<div class="flex items-start gap-4">
							<div class="flex-shrink-0 w-11 h-11 rounded-lg bg-orange-500/10 border border-orange-500/20 flex items-center justify-center group-hover:bg-orange-500/20 transition-colors">
								<svg class="w-5 h-5 text-orange-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
									{@html adv.icon}
								</svg>
							</div>
							<div>
								<h3 class="text-white font-semibold mb-2 leading-snug">{adv.title}</h3>
								<p class="text-gray-500 text-sm leading-relaxed">{adv.desc}</p>
							</div>
						</div>
					</div>
				</div>
			{/each}
		</div>

		<!-- Comparison CTA -->
		<div class="mt-16 text-center fade-in">
			<div class="inline-block bg-[#1a1a1a] border border-[#2a2a2a] rounded-2xl px-8 py-6 text-center">
				<p class="text-gray-400 mb-4">
					Kíváncsi, hogy gyorsabb-e a homokszórástól?
					<span class="text-blue-400">Sok esetben igen – és tisztább is.</span>
				</p>
				<a href="#kapcsolat" class="btn-primary inline-flex">
					Tudjon meg többet
				</a>
			</div>
		</div>
	</div>
</section>
