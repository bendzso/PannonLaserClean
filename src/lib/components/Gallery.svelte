<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	type GalleryItem =
		| { type: 'image'; src: string; alt: string; span?: string }
		| { type: 'youtube'; videoId: string; alt: string; span?: string };

	const items: GalleryItem[] = [
		{ type: 'youtube', videoId: 'SXeeRgEY2UE', alt: 'Lézertisztítás videó 1', span: 'col-span-2 row-span-2' },
		{ type: 'image',   src: '/gallery/image-01.jpg',  alt: 'Lézertisztítás – 1' },
		{ type: 'image',   src: '/gallery/image-02.webp', alt: 'Lézertisztítás – 2' },
		{ type: 'image',   src: '/gallery/image-03.webp', alt: 'Lézertisztítás – 3' },
		{ type: 'image',   src: '/gallery/image-04.webp', alt: 'Lézertisztítás – 4' },
		{ type: 'youtube', videoId: 'IkzPEzGcQx0', alt: 'Lézertisztítás videó 2', span: 'col-span-2' },
		{ type: 'image',   src: '/gallery/image-05.webp', alt: 'Lézertisztítás – 5' },
		{ type: 'image',   src: '/gallery/image-06.png',  alt: 'Lézertisztítás – 6' },
		{ type: 'image',   src: '/gallery/image-07.jpeg', alt: 'Lézertisztítás – 7' },
		{ type: 'image',   src: '/gallery/image-08.jpg',  alt: 'Lézertisztítás – 8' },
	];

	function ytThumb(id: string) {
		return `https://img.youtube.com/vi/${id}/maxresdefault.jpg`;
	}

	function ytEmbed(id: string) {
		return `https://www.youtube.com/embed/${id}?autoplay=1&rel=0`;
	}

	let lightbox = $state<{ open: boolean; index: number }>({ open: false, index: 0 });

	function openLightbox(i: number) {
		lightbox = { open: true, index: i };
		document.body.style.overflow = 'hidden';
	}

	function closeLightbox() {
		lightbox = { open: false, index: 0 };
		document.body.style.overflow = '';
	}

	function prev() {
		lightbox.index = (lightbox.index - 1 + items.length) % items.length;
	}

	function next() {
		lightbox.index = (lightbox.index + 1) % items.length;
	}

	function onKey(e: KeyboardEvent) {
		if (!lightbox.open) return;
		if (e.key === 'Escape') closeLightbox();
		if (e.key === 'ArrowLeft') prev();
		if (e.key === 'ArrowRight') next();
	}

	onMount(() => {
		const obs = new IntersectionObserver(
			(entries) => entries.forEach(e => e.target.classList.toggle('visible', e.isIntersecting)),
			{ threshold: 0.05 }
		);
		section.querySelectorAll('.fade-in').forEach(el => obs.observe(el));
		return () => obs.disconnect();
	});
</script>

<svelte:window onkeydown={onKey} />

<section id="galeria" class="py-24 lg:py-32 relative" bind:this={section}>
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">

		<div class="text-center mb-16 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Galéria</h2>
			<p class="text-gray-500">Munkáink – fotók és videók a lézertisztítás eredményeiről</p>
		</div>

		<div class="grid grid-cols-2 lg:grid-cols-4 gap-3 auto-rows-[180px] lg:auto-rows-[200px]">
			{#each items as item, i}
				<button
					class="fade-in relative overflow-hidden rounded-xl bg-[#1a1a1a] border border-[#2a2a2a] group cursor-pointer {item.span ?? ''}"
					style="transition-delay: {i * 0.05}s;"
					onclick={() => openLightbox(i)}
					aria-label="Nagyítás: {item.alt}"
				>
					{#if item.type === 'youtube'}
						<img
							src={ytThumb(item.videoId)}
							alt={item.alt}
							class="absolute inset-0 w-full h-full object-cover"
						/>
						<div class="absolute inset-0 bg-black/40 group-hover:bg-black/20 transition-all"></div>
						<div class="absolute inset-0 flex items-center justify-center">
							<div class="w-14 h-14 rounded-full bg-red-600/90 border-2 border-white/30 flex items-center justify-center group-hover:scale-110 transition-transform shadow-xl">
								<svg class="w-6 h-6 text-white ml-1" fill="currentColor" viewBox="0 0 24 24">
									<path d="M8 5v14l11-7z"/>
								</svg>
							</div>
						</div>
					{:else}
						<img
							src={item.src}
							alt={item.alt}
							class="absolute inset-0 w-full h-full object-cover group-hover:scale-105 transition-transform duration-500"
						/>
						<div class="absolute inset-0 bg-black/0 group-hover:bg-black/20 transition-all duration-300"></div>
					{/if}

					<div class="absolute bottom-0 left-0 right-0 p-3 bg-gradient-to-t from-black/70 to-transparent opacity-0 group-hover:opacity-100 transition-opacity">
						<p class="text-white text-xs font-medium">{item.alt}</p>
					</div>
				</button>
			{/each}
		</div>
	</div>
</section>

<!-- Lightbox -->
{#if lightbox.open}
	<!-- svelte-ignore a11y_click_events_have_key_events a11y_no_static_element_interactions -->
	<div
		class="fixed inset-0 z-[100] bg-black/95 flex items-center justify-center p-4"
		onclick={(e) => e.target === e.currentTarget && closeLightbox()}
	>
		<button
			class="absolute top-4 right-4 w-10 h-10 rounded-full bg-white/10 hover:bg-white/20 flex items-center justify-center text-white transition-colors"
			onclick={closeLightbox}
			aria-label="Bezárás"
		>
			<svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
			</svg>
		</button>

		<button
			class="absolute left-4 top-1/2 -translate-y-1/2 w-10 h-10 rounded-full bg-white/10 hover:bg-white/20 flex items-center justify-center text-white transition-colors"
			onclick={prev}
			aria-label="Előző"
		>
			<svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/>
			</svg>
		</button>

		<div class="max-w-4xl w-full mx-12">
			{#if items[lightbox.index].type === 'youtube'}
				<div class="relative w-full rounded-xl overflow-hidden" style="padding-top: 56.25%;">
					<iframe
						src={ytEmbed((items[lightbox.index] as { type: 'youtube'; videoId: string }).videoId)}
						class="absolute inset-0 w-full h-full"
						frameborder="0"
						allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
						allowfullscreen
						title={items[lightbox.index].alt}
					></iframe>
				</div>
			{:else}
				<img
					src={(items[lightbox.index] as { type: 'image'; src: string }).src}
					alt={items[lightbox.index].alt}
					class="w-full rounded-xl max-h-[80vh] object-contain"
				/>
			{/if}
			<p class="text-gray-400 text-sm text-center mt-4">{items[lightbox.index].alt}</p>
			<p class="text-gray-600 text-xs text-center">{lightbox.index + 1} / {items.length}</p>
		</div>

		<button
			class="absolute right-4 top-1/2 -translate-y-1/2 w-10 h-10 rounded-full bg-white/10 hover:bg-white/20 flex items-center justify-center text-white transition-colors"
			onclick={next}
			aria-label="Következő"
		>
			<svg class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/>
			</svg>
		</button>
	</div>
{/if}
