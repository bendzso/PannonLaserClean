<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	const faqs = [
		{
			q: 'Milyen felületek tisztíthatók lézerrel?',
			a: 'A legtöbb fém, fa és egyes műanyag felületek is tisztíthatók. A technológia különösen hatékony rozsda, festék és oxidáció eltávolítására.',
		},
		{
			q: 'Nem károsítja a lézer az anyagot?',
			a: 'Nem. A megfelelő beállításokkal a lézer csak a szennyeződést távolítja el, az alapfelület sértetlen marad. Ez az egyik legnagyobb előnye a hagyományos módszerekkel szemben.',
		},
		{
			q: 'Mennyire veszélyes a lézeres tisztítás?',
			a: 'A folyamat biztonságos, megfelelő védőfelszereléssel történik. A munkavégzés során minden szükséges biztonsági előírást betartunk.',
		},
		{
			q: 'Helyszínen is elvégezhető a munka?',
			a: 'Igen, szolgáltatásunk mobil. A legtöbb munkát közvetlenül az Ön telephelyén végezzük el – nem kell szállítani az alkatrészeket.',
		},
		{
			q: 'Mennyibe kerül egy tisztítás?',
			a: 'Az ár a felület méretétől, állapotától és a szennyeződés típusától függ. Előzetes árajánlatot minden esetben adunk – küldjön fotót, és rövid időn belül visszajelzünk.',
		},
		{
			q: 'Gyorsabb, mint a homokszórás?',
			a: 'Sok esetben igen, különösen precíz vagy kisebb munkáknál. Emellett tisztább és környezetbarátabb megoldás, mivel nem keletkezik homok- vagy vegyszermaradék.',
		},
	];

	let open = $state<number | null>(null);

	function toggle(i: number) {
		open = open === i ? null : i;
	}

	onMount(() => {
		const obs = new IntersectionObserver(
			(entries) => entries.forEach(e => e.target.classList.toggle('visible', e.isIntersecting)),
			{ threshold: 0.1 }
		);
		section.querySelectorAll('.fade-in').forEach(el => obs.observe(el));
		return () => obs.disconnect();
	});
</script>

<section id="gyik" class="py-24 lg:py-32 relative" bind:this={section}>
	<div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">

		<div class="text-center mb-16 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Gyakori kérdések</h2>
			<p class="text-gray-500">Amit a legtöbben megkérdeznek</p>
		</div>

		<div class="space-y-3">
			{#each faqs as faq, i}
				<div class="fade-in" style="transition-delay: {i * 0.07}s;">
					<button
						class="w-full text-left bg-[#1a1a1a] border rounded-xl overflow-hidden transition-all duration-300"
						style="border-color: {open === i ? '#f97316' : '#2a2a2a'};"
						onclick={() => toggle(i)}
					>
						<div class="flex items-center justify-between px-6 py-5 gap-4">
							<span class="text-white font-medium text-sm lg:text-base">{faq.q}</span>
							<span
								class="flex-shrink-0 w-7 h-7 rounded-full border flex items-center justify-center transition-all duration-300"
								style="
									border-color: {open === i ? '#f97316' : '#3b82f6'};
									color: {open === i ? '#f97316' : '#3b82f6'};
									transform: rotate({open === i ? 45 : 0}deg);
								"
							>
								<svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/>
								</svg>
							</span>
						</div>

						{#if open === i}
							<div class="px-6 pb-5 text-gray-400 text-sm leading-relaxed border-t border-[#2a2a2a]" style="padding-top: 1rem;">
								{faq.a}
							</div>
						{/if}
					</button>
				</div>
			{/each}
		</div>

		<div class="text-center mt-12 fade-in">
			<p class="text-gray-500 mb-4">Más kérdése van?</p>
			<a href="#kapcsolat" class="btn-outline">
				Írjon nekünk
				<svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
				</svg>
			</a>
		</div>
	</div>
</section>
