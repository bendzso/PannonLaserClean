<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	// TODO: cseréld le tényleges előtte/utána képpárokra
	const pairs = [
		{
			title: 'Rozsdás fém alkatrész',
			before: '/gallery/before1.jpg',
			after: '/gallery/after1.jpg',
		},
		{
			title: 'Festett acél felület',
			before: '/gallery/before2.jpg',
			after: '/gallery/after2.jpg',
		},
		{
			title: 'Mezőgazdasági gép',
			before: '/gallery/before3.jpg',
			after: '/gallery/after3.jpg',
		},
	];

	let sliders = $state(pairs.map(() => 50));

	let dragging = $state<number | null>(null);

	function startDrag(i: number) {
		dragging = i;
	}

	function onMove(e: MouseEvent | TouchEvent, i: number) {
		if (dragging !== i) return;
		const el = (e.currentTarget as HTMLElement).closest('.slider-wrap') as HTMLElement;
		if (!el) return;
		const rect = el.getBoundingClientRect();
		const clientX = e instanceof MouseEvent ? e.clientX : e.touches[0].clientX;
		const pct = Math.max(0, Math.min(100, ((clientX - rect.left) / rect.width) * 100));
		sliders[i] = pct;
	}

	function stopDrag() {
		dragging = null;
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

<svelte:window onmouseup={stopDrag} ontouchend={stopDrag} />

<section id="elotte-utana" class="py-24 lg:py-32 bg-[#0c0c0c] relative" bind:this={section}>
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">

		<div class="text-center mb-16 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Előtte / Utána</h2>
			<p class="text-gray-500">Húzza a csúszkát a különbség megtekintéséhez</p>
		</div>

		<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
			{#each pairs as pair, i}
				<div class="fade-in" style="transition-delay: {i * 0.12}s;">
					<!-- svelte-ignore a11y_no_static_element_interactions -->
					<div
						class="slider-wrap relative rounded-xl overflow-hidden border border-[#2a2a2a] aspect-[4/3] cursor-col-resize select-none bg-[#1a1a1a]"
						onmousemove={(e) => onMove(e, i)}
						ontouchmove={(e) => onMove(e, i)}
					>
						<!-- AFTER (base layer) -->
						<div class="absolute inset-0 flex items-center justify-center">
							<svg class="w-12 h-12 text-blue-500/20" fill="none" viewBox="0 0 24 24" stroke="currentColor">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"/>
							</svg>
						</div>
						<div class="absolute bottom-2 right-3 text-xs font-semibold text-blue-400 bg-blue-400/10 px-2 py-0.5 rounded">UTÁNA</div>

						<!-- BEFORE (clip layer) -->
						<div
							class="absolute inset-0 overflow-hidden"
							style="clip-path: inset(0 {100 - sliders[i]}% 0 0);"
						>
							<div class="absolute inset-0 bg-[#111] flex items-center justify-center">
								<svg class="w-12 h-12 text-orange-500/20" fill="none" viewBox="0 0 24 24" stroke="currentColor">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"/>
								</svg>
							</div>
							<div class="absolute bottom-2 left-3 text-xs font-semibold text-orange-400 bg-orange-400/10 px-2 py-0.5 rounded">ELŐTTE</div>
						</div>

						<!-- Divider line + handle -->
						<div
							class="absolute top-0 bottom-0 z-10 flex items-center justify-center pointer-events-none"
							style="left: {sliders[i]}%; transform: translateX(-50%);"
						>
							<div class="w-0.5 h-full bg-white/60"></div>
							<button
								class="absolute w-9 h-9 rounded-full bg-white flex items-center justify-center shadow-xl pointer-events-auto"
								style="cursor: col-resize;"
								onmousedown={() => startDrag(i)}
								ontouchstart={() => startDrag(i)}
								aria-label="Húzza a csúszkát"
							>
								<svg class="w-5 h-5 text-gray-800" fill="none" viewBox="0 0 24 24" stroke="currentColor">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 9l-3 3 3 3M16 9l3 3-3 3"/>
								</svg>
							</button>
						</div>
					</div>
					<p class="text-gray-400 text-sm text-center mt-3">{pair.title}</p>
				</div>
			{/each}
		</div>
	</div>
</section>
