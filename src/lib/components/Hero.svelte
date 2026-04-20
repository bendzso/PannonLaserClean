<script lang="ts">
	const checks = [
		'Rozsda eltávolítás',
		'Festék és bevonatok tisztítása',
		'Ipari és lakossági felületek',
		'Mobil, helyszíni szolgáltatás',
	];
</script>

<section id="hero" class="relative min-h-screen flex items-center justify-center overflow-hidden pt-20">
	<!-- Gradient overlay -->
	<div class="absolute inset-0 pointer-events-none" style="
		background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(249,115,22,0.07) 0%, transparent 60%),
		            radial-gradient(ellipse 60% 40% at 80% 80%, rgba(59,130,246,0.06) 0%, transparent 50%);
		z-index: 1;
	"></div>

	<div class="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-24 lg:py-32" style="z-index: 2;">
		<div class="max-w-3xl">

			<!-- Badge -->
			<div class="inline-flex items-center gap-2 px-3 py-1.5 rounded-full border border-orange-500/30 bg-orange-500/10 mb-6">
				<span class="w-2 h-2 rounded-full bg-orange-500 animate-pulse"></span>
				<span class="text-orange-400 text-xs font-semibold uppercase tracking-widest">Dél-Dunántúl · Baranya megye</span>
			</div>

			<!-- Title -->
			<h1 class="section-title text-white mb-4" style="font-size: clamp(2.5rem, 6vw, 4rem); line-height: 1.1;">
				<span class="text-white">Pannon</span><br>
				<span class="text-orange-500 glow-orange">Laser Clean</span>
			</h1>

			<p class="text-xl lg:text-2xl text-gray-400 font-medium mb-8 max-w-2xl" style="line-height: 1.5;">
				Modern lézeres tisztítás Baranyában és a Dél-Dunántúlon
			</p>

			<p class="text-gray-500 text-base lg:text-lg mb-10 max-w-xl">
				Professzionális, érintésmentes tisztítás fém, fa és egyéb felületeken – gyorsan, vegyszerek nélkül, károsodás nélkül.
			</p>

			<!-- Checkmarks -->
			<ul class="grid grid-cols-1 sm:grid-cols-2 gap-3 mb-12">
				{#each checks as item}
					<li class="flex items-center gap-2.5 text-gray-300 text-sm lg:text-base">
						<span class="flex-shrink-0 w-5 h-5 rounded-full bg-orange-500/20 border border-orange-500/40 flex items-center justify-center">
							<svg class="w-3 h-3 text-orange-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"/>
							</svg>
						</span>
						{item}
					</li>
				{/each}
			</ul>

			<!-- CTAs -->
			<div class="flex flex-col sm:flex-row gap-4">
				<a href="#kapcsolat" class="btn-primary text-base">
					Kérjen ajánlatot még ma
					<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"/>
					</svg>
				</a>
				<a href="#galeria" class="btn-outline text-base">
					Eredményeink
					<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"/>
					</svg>
				</a>
			</div>
		</div>
	</div>

	<!-- Scroll indicator -->
	<div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 opacity-50" style="z-index: 2;">
		<span class="text-gray-500 text-xs uppercase tracking-widest">Görgessen</span>
		<div class="w-px h-12 bg-gradient-to-b from-orange-500/60 to-transparent"></div>
	</div>
</section>
