<script lang="ts">
	import { onMount } from 'svelte';
	import emailjs from '@emailjs/browser';

	let section: HTMLElement;

	let form = $state({
		email: '',
		nev: '',
		telefon: '',
		cim: '',
		helyszin: '',
		leiras: '',
	});

	let errors = $state<Record<string, string>>({});
	let status = $state<'idle' | 'sending' | 'success' | 'error'>('idle');

	function validate() {
		const e: Record<string, string> = {};
		if (!form.email.trim()) e.email = 'Az e-mail cím megadása kötelező.';
		else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) e.email = 'Érvényes e-mail címet adjon meg.';
		if (!form.helyszin) e.helyszin = 'A munkavégzés helyszínét kötelező kiválasztani.';
		return e;
	}

	async function submit(e: SubmitEvent) {
		e.preventDefault();
		errors = validate();
		if (Object.keys(errors).length > 0) return;

		status = 'sending';

		try {
			await emailjs.send(
				import.meta.env.VITE_EMAILJS_SERVICE_ID,
				import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
				{
					from_email: form.email,
					from_name: form.nev || 'Névtelen',
					telefon: form.telefon,
					cim: form.cim,
					helyszin: form.helyszin,
					leiras: form.leiras,
				},
				import.meta.env.VITE_EMAILJS_PUBLIC_KEY
			);
			status = 'success';
			form = { email: '', nev: '', telefon: '', cim: '', helyszin: '', leiras: '' };
		} catch {
			status = 'error';
		}
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

<section id="kapcsolat" class="py-24 lg:py-32 relative" bind:this={section}>
	<!-- Gradient -->
	<div class="absolute inset-0 pointer-events-none" style="
		background: radial-gradient(ellipse 60% 50% at 50% 100%, rgba(249,115,22,0.06) 0%, transparent 60%);
	"></div>

	<div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 relative">

		<div class="text-center mb-12 fade-in">
			<div class="orange-line mx-auto"></div>
			<h2 class="section-title text-white mb-4">Ajánlatkérés</h2>
			<p class="text-gray-500">
				Töltse ki az alábbi űrlapot, és hamarosan felvesszük Önnel a kapcsolatot.
			</p>
		</div>

		<div class="card fade-in" style="padding: 2rem; transition-delay: 0.1s;">

			{#if status === 'success'}
				<div class="text-center py-10">
					<div class="w-16 h-16 rounded-full bg-green-500/20 border-2 border-green-500/50 flex items-center justify-center mx-auto mb-5">
						<svg class="w-8 h-8 text-green-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
						</svg>
					</div>
					<h3 class="text-white text-xl font-bold mb-2">Köszönjük az ajánlatkérést!</h3>
					<p class="text-gray-400 mb-6">Rövid időn belül visszajelzünk az <strong class="text-orange-400">info@pannonlaserclean.hu</strong> e-mail-ről.</p>
					<button class="btn-outline" onclick={() => status = 'idle'}>Új ajánlatkérés</button>
				</div>

			{:else}
				<form onsubmit={submit} novalidate class="space-y-5">

					<!-- Email + Név -->
					<div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
						<div>
							<label for="f-email" class="block text-sm font-medium text-gray-300 mb-1.5">
								E-mail cím <span class="text-orange-500">*</span>
							</label>
							<input
								id="f-email"
								type="email"
								bind:value={form.email}
								placeholder="pelda@email.hu"
								class="w-full bg-[#111] border rounded-lg px-4 py-3 text-white text-sm placeholder-gray-600 outline-none transition-colors focus:border-orange-500"
								style="border-color: {errors.email ? '#ef4444' : '#2a2a2a'};"
							/>
							{#if errors.email}<p class="mt-1 text-red-400 text-xs">{errors.email}</p>{/if}
						</div>

						<div>
							<label for="f-nev" class="block text-sm font-medium text-gray-300 mb-1.5">Név</label>
							<input
								id="f-nev"
								type="text"
								bind:value={form.nev}
								placeholder="Kovács János"
								class="w-full bg-[#111] border border-[#2a2a2a] rounded-lg px-4 py-3 text-white text-sm placeholder-gray-600 outline-none transition-colors focus:border-blue-500"
							/>
						</div>
					</div>

					<!-- Telefon + Cím -->
					<div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
						<div>
							<label for="f-telefon" class="block text-sm font-medium text-gray-300 mb-1.5">Telefonszám</label>
							<input
								id="f-telefon"
								type="tel"
								bind:value={form.telefon}
								placeholder="+36 30 123 4567"
								class="w-full bg-[#111] border border-[#2a2a2a] rounded-lg px-4 py-3 text-white text-sm placeholder-gray-600 outline-none transition-colors focus:border-blue-500"
							/>
						</div>

						<div>
							<label for="f-cim" class="block text-sm font-medium text-gray-300 mb-1.5">Cím</label>
							<input
								id="f-cim"
								type="text"
								bind:value={form.cim}
								placeholder="7621 Pécs, Példa utca 1."
								class="w-full bg-[#111] border border-[#2a2a2a] rounded-lg px-4 py-3 text-white text-sm placeholder-gray-600 outline-none transition-colors focus:border-blue-500"
							/>
						</div>
					</div>

					<!-- Munkavégzés helyszíne -->
					<div>
						<p class="block text-sm font-medium text-gray-300 mb-1.5">
							Munkavégzés <span class="text-orange-500">*</span>
						</p>
						<div class="grid grid-cols-2 gap-3">
							{#each ['Helyszínen', 'Házhozszállítva'] as opt}
								<button
									type="button"
									class="py-3 px-4 rounded-lg border text-sm font-medium transition-all"
									style="
										border-color: {form.helyszin === opt ? '#f97316' : '#2a2a2a'};
										background: {form.helyszin === opt ? 'rgba(249,115,22,0.12)' : '#111'};
										color: {form.helyszin === opt ? '#f97316' : '#6b7280'};
									"
									onclick={() => { form.helyszin = opt; errors.helyszin = ''; }}
								>
									{opt}
								</button>
							{/each}
						</div>
						{#if errors.helyszin}<p class="mt-1 text-red-400 text-xs">{errors.helyszin}</p>{/if}
					</div>

					<!-- Leírás -->
					<div>
						<label for="f-leiras" class="block text-sm font-medium text-gray-300 mb-1.5">Leírás / Megjegyzés</label>
						<textarea
							id="f-leiras"
							bind:value={form.leiras}
							rows="4"
							placeholder="Írja le röviden, mit szeretne tisztíttatni – ha tud, csatoljon fotót e-mailben."
							class="w-full bg-[#111] border border-[#2a2a2a] rounded-lg px-4 py-3 text-white text-sm placeholder-gray-600 outline-none transition-colors focus:border-blue-500 resize-none"
						></textarea>
					</div>

					<!-- Error notice -->
					{#if status === 'error'}
						<div class="bg-red-500/10 border border-red-500/30 rounded-lg px-4 py-3 text-red-400 text-sm">
							Hiba történt a küldés során. Kérjük, próbálja újra, vagy írjon közvetlenül az <a href="mailto:info@pannonlaserclean.hu" class="underline">info@pannonlaserclean.hu</a> címre.
						</div>
					{/if}

					<button
						type="submit"
						class="btn-primary w-full justify-center text-base py-4"
						disabled={status === 'sending'}
					>
						{#if status === 'sending'}
							<svg class="animate-spin w-5 h-5" fill="none" viewBox="0 0 24 24">
								<circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
								<path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"></path>
							</svg>
							Küldés...
						{:else}
							Ajánlatkérés elküldése
							<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"/>
							</svg>
						{/if}
					</button>

					<p class="text-center text-gray-600 text-xs">
						Az üzenet az <strong class="text-gray-500">info@pannonlaserclean.hu</strong> e-mail-re érkezik. A csillaggal (*) jelölt mezők kitöltése kötelező.
					</p>
				</form>
			{/if}
		</div>
	</div>
</section>
