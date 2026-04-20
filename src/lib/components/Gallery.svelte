<script lang="ts">
	import { onMount } from 'svelte';

	let section: HTMLElement;

	// TODO: cseréld le a tényleges képek/videók elérési útjára
	const items = [
		{ type: 'image', src: '/gallery/photo1.jpg', alt: 'Rozsdaeltávolítás fém alkatrészről', span: 'col-span-2 row-span-2' },
		{ type: 'image', src: '/gallery/photo2.jpg', alt: 'Festék eltávolítása' },
		{ type: 'video', src: '/gallery/video1.mp4', thumb: '/gallery/thumb1.jpg', alt: 'Lézertisztítás folyamata' },
		{ type: 'image', src: '/gallery/photo3.jpg', alt: 'Ipari berendezés tisztítása' },
		{ type: 'image', src: '/gallery/photo4.jpg', alt: 'Mezőgazdasági gép alkatrész' },
		{ type: 'video', src: '/gallery/video2.mp4', thumb: '/gallery/thumb2.jpg', alt: 'Rozsda eltávolítás' },
		{ type: 'image', src: '/gallery/photo5.jpg', alt: 'Autóipari alkatrész' },
		{ type: 'image', src: '/gallery/photo6.jpg', alt: 'Fa felület restaurálás' },
	] as { type: 'image' | 'video'; src: string; thumb?: string; alt: string; span?: string }[];

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

		<!-- Grid -->
		<div class="grid grid-cols-2 lg:grid-cols-4 gap-3 auto-rows-[180px] lg:auto-rows-[200px]">
			{#each items as item, i}
				<button
					class="fade-in relative overflow-hidden rounded-xl bg-[#1a1a1a] border border-[#2a2a2a] group cursor-pointer {item.span ?? ''}"
					style="transition-delay: {i * 0.05}s;"
					onclick={() => openLightbox(i)}
					aria-label="Nagyítás: {item.alt}"
				>
					{#if item.type === 'video'}
						<!-- Video thumbnail placeholder -->
						<div class="absolute inset-0 flex flex-col items-center justify-center bg-[#111]">
							<div class="w-14 h-14 rounded-full bg-orange-500/20 border-2 border-orange-500/50 flex items-center justify-center group-hover:bg-orange-500/40 transition-all">
								<svg class="w-6 h-6 text-orange-400 ml-1" fill="currentColor" viewBox="0 0 24 24">
									<path d="M8 5v14l11-7z"/>
								</svg>
							</div>
							<span class="mt-2 text-gray-500 text-xs">Videó</span>
						</div>
					{:else}
						<!-- Image placeholder -->
						<div class="absolute inset-0 flex flex-col items-center justify-center bg-[#111]">
							<svg class="w-10 h-10 text-gray-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"/>
							</svg>
						</div>
					{/if}

					<!-- Hover overlay -->
					<div class="absolute inset-0 bg-orange-500/0 group-hover:bg-orange-500/10 transition-all duration-300"></div>

					<!-- Label -->
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
		class="fixed inset-0 z-[100] bg-black/90 flex items-center justify-center p-4"
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
			{#if items[lightbox.index].type === 'video'}
				<video
					src={items[lightbox.index].src}
					class="w-full rounded-xl max-h-[80vh]"
					controls
					autoplay
				>
					<track kind="captions" />
				</video>
			{:else}
				<div class="w-full aspect-[16/10] rounded-xl bg-[#1a1a1a] flex items-center justify-center">
					<svg class="w-20 h-20 text-gray-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"/>
					</svg>
				</div>
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
