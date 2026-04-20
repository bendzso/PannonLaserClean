<script lang="ts">
	import { onMount } from "svelte";

	let section: HTMLElement;

	onMount(() => {
		const obs = new IntersectionObserver(
			(entries) =>
				entries.forEach((e) =>
					e.target.classList.toggle("visible", e.isIntersecting),
				),
			{ threshold: 0.15 },
		);
		section.querySelectorAll(".fade-in").forEach((el) => obs.observe(el));
		return () => obs.disconnect();
	});
</script>

<section id="bemutatkozas" class="py-24 lg:py-32 relative" bind:this={section}>
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="grid lg:grid-cols-2 gap-16 items-center">
			<!-- Text -->
			<div class="fade-in">
				<div class="orange-line"></div>
				<h2 class="section-title text-white mb-6">Rólunk</h2>
				<p class="text-gray-400 text-lg mb-6 leading-relaxed">
					A <strong class="text-orange-400">Pannon Laser Clean</strong
					> célja, hogy a legmodernebb lézertechnológiát elérhetővé tegye
					helyi vállalkozások és magánszemélyek számára.
				</p>
				<p class="text-gray-500 mb-8 leading-relaxed">
					A lézeres tisztítás egy innovatív megoldás, amely precízen
					távolítja el a szennyeződéseket anélkül, hogy károsítaná az
					alapanyagot. Nincs szükség vegyszerekre, nincs másodlagos
					hulladék – csak tiszta felület.
				</p>
				<p class="text-gray-500 leading-relaxed">
					Szolgáltatásunk <strong class="text-blue-400">mobil</strong
					>, így a munkát közvetlenül az Ön telephelyén vagy
					otthonában végezzük el.
				</p>

				<div class="mt-10 flex flex-wrap gap-6">
					<div class="text-center">
						<div class="text-3xl font-bold text-orange-500">
							100%
						</div>
						<div class="text-gray-500 text-sm mt-1">
							Vegyszermentes
						</div>
					</div>
					<div class="w-px bg-[#2a2a2a]"></div>
					<div class="text-center">
						<div class="text-3xl font-bold text-blue-400">0</div>
						<div class="text-gray-500 text-sm mt-1">
							Másodlagos hulladék
						</div>
					</div>
					<div class="w-px bg-[#2a2a2a]"></div>
					<div class="text-center">
						<div class="text-3xl font-bold text-orange-500">
							Mobil
						</div>
						<div class="text-gray-500 text-sm mt-1">
							Helyszíni szolgáltatás
						</div>
					</div>
				</div>
			</div>

			<!-- Visual -->
			<div class="fade-in" style="transition-delay: 0.2s;">
				<div
					class="relative rounded-2xl overflow-hidden border border-[#2a2a2a] bg-[#1a1a1a] aspect-square flex items-center justify-center"
				>
					<!-- Placeholder for image -->
					<div
						class="absolute inset-0 flex flex-col items-center justify-center text-center p-8"
					>
						<img
							src="gallery/hero.jpg"
							alt="Pannon Laser Clean – lézertisztítás"
							class="w-full h-full object-cover"
						/>
					</div>
					<!-- Decorative corner lines -->
					<div
						class="absolute top-0 left-0 w-8 h-8 border-t-2 border-l-2 border-orange-500/50 rounded-tl-2xl"
					></div>
					<div
						class="absolute bottom-0 right-0 w-8 h-8 border-b-2 border-r-2 border-blue-500/50 rounded-br-2xl"
					></div>
				</div>
			</div>
		</div>
	</div>
</section>
