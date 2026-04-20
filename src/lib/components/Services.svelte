<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	const services = [
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"/>`,
			title: 'Fém alkatrészek',
			desc: 'Rozsda, oxidáció és korróziós rétegek hatékony eltávolítása bármilyen fémfelületről.',
			accent: 'orange',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zm0 0h12a2 2 0 002-2v-4a2 2 0 00-2-2h-2.343M11 7.343l1.657-1.657a2 2 0 012.828 0l2.829 2.829a2 2 0 010 2.828l-8.486 8.485M7 17h.01"/>`,
			title: 'Festett felületek',
			desc: 'Régi bevonatok, festékrétegek precíz eltávolítása az alapfelület sérülése nélkül.',
			accent: 'blue',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z"/>`,
			title: 'Fa felületek',
			desc: 'Fa restaurálás és tisztítás: szürküléstől a mohától és penésztől megtisztítva.',
			accent: 'orange',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"/><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>`,
			title: 'Ipari berendezések',
			desc: 'Gépek, berendezések karbantartási célú tisztítása leállás minimalizálásával.',
			accent: 'blue',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M3.055 11H5a2 2 0 012 2v1a2 2 0 002 2 2 2 0 012 2v2.945M8 3.935V5.5A2.5 2.5 0 0010.5 8h.5a2 2 0 012 2 2 2 0 104 0 2 2 0 012-2h1.064M15 20.488V18a2 2 0 012-2h3.064M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>`,
			title: 'Mezőgazdasági gépek',
			desc: 'Traktoros, kombájnos és egyéb mezőgazdasági gépelemek tisztítása helyszínen.',
			accent: 'orange',
		},
		{
			icon: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 3H5a2 2 0 00-2 2v4m6-6h10a2 2 0 012 2v4M9 3v18m0 0h10a2 2 0 002-2V9M9 21H5a2 2 0 01-2-2V9m0 0h18"/>`,
			title: 'Autóipari alkatrészek',
			desc: 'Karosszéria, alváz, fékdob és egyéb alkatrészek rozsda- és festékmentesítése.',
			accent: 'blue',
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

<section id="szolgaltatasok" class="py-24 lg:py-32 bg-[#0c0c0c] relative" bind:this={section}>
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">

		<div class="text-center mb-16 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Mit tisztítunk?</h2>
			<p class="text-gray-500 max-w-xl mx-auto">
				Ha nem biztos benne, hogy az Ön felülete tisztítható-e –
				<a href="#kapcsolat" class="text-orange-400 hover:text-orange-300 underline underline-offset-2">küldjön képet, és segítünk!</a>
			</p>
		</div>

		<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
			{#each services as svc, i}
				<div class="card fade-in" style="transition-delay: {i * 0.08}s;">
					<div class="w-12 h-12 rounded-xl mb-5 flex items-center justify-center"
						style="background: {svc.accent === 'orange' ? 'rgba(249,115,22,0.12)' : 'rgba(59,130,246,0.12)'};">
						<svg class="w-6 h-6" style="color: {svc.accent === 'orange' ? '#f97316' : '#3b82f6'};"
							fill="none" viewBox="0 0 24 24" stroke="currentColor">
							{@html svc.icon}
						</svg>
					</div>
					<h3 class="text-white font-bold text-lg mb-2">{svc.title}</h3>
					<p class="text-gray-500 text-sm leading-relaxed">{svc.desc}</p>
				</div>
			{/each}
		</div>
	</div>
</section>
