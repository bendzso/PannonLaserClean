<script lang="ts">
	const year = new Date().getFullYear();
</script>

<footer class="bg-[#080808] border-t border-[#1e1e1e] py-12 relative">
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="grid grid-cols-1 md:grid-cols-3 gap-10 mb-10">
			<!-- Brand -->
			<div>
				<div class="flex items-center gap-3 mb-4">
					<img
						src="/gallery/logo.png"
						alt="Pannon Laser Clean logó"
						class="h-18 w-auto rounded-lg"
					/>
				</div>
				<p class="text-gray-600 text-sm leading-relaxed">
					Professzionális lézertisztítás Baranyában és a
					Dél-Dunántúlon.
				</p>
				<p class="text-gray-700 text-xs mt-3">
					Tiszta felület, kompromisszumok nélkül.
				</p>
			</div>

			<!-- Navigation -->
			<div>
				<h4 class="text-white text-sm font-semibold mb-4">Navigáció</h4>
				<ul class="space-y-2">
					{#each [{ label: "Bemutatkozás", href: "#bemutatkozas" }, { label: "Szolgáltatások", href: "#szolgaltatasok" }, { label: "Miért lézer?", href: "#miert-lezer" }, { label: "Galéria", href: "#galeria" }, { label: "Hogyan dolgozunk", href: "#hogyan-dolgozunk" }, { label: "GYIK", href: "#gyik" }, { label: "Ajánlatkérés", href: "#kapcsolat" }] as link}
						<li>
							<a
								href={link.href}
								class="text-gray-600 text-sm hover:text-orange-400 transition-colors"
							>
								{link.label}
							</a>
						</li>
					{/each}
				</ul>
			</div>

			<!-- Contact -->
			<div>
				<h4 class="text-white text-sm font-semibold mb-4">Kapcsolat</h4>
				<ul class="space-y-3">
					<li class="flex items-center gap-3">
						<div
							class="w-8 h-8 rounded-lg bg-orange-500/10 flex items-center justify-center flex-shrink-0"
						>
							<svg
								class="w-4 h-4 text-orange-500"
								fill="none"
								viewBox="0 0 24 24"
								stroke="currentColor"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
								/>
							</svg>
						</div>
						<a
							href="mailto:info@pannonlaserclean.hu"
							class="text-gray-400 text-sm hover:text-orange-400 transition-colors"
						>
							info@pannonlaserclean.hu
						</a>
					</li>
					<li class="flex items-center gap-3">
						<div
							class="w-8 h-8 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0"
						>
							<svg
								class="w-4 h-4 text-blue-400"
								fill="none"
								viewBox="0 0 24 24"
								stroke="currentColor"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
								/>
							</svg>
						</div>
						<span class="text-gray-500 text-sm">(telefonszám)</span>
					</li>
					<li class="flex items-center gap-3">
						<div
							class="w-8 h-8 rounded-lg bg-orange-500/10 flex items-center justify-center flex-shrink-0"
						>
							<svg
								class="w-4 h-4 text-orange-400"
								fill="none"
								viewBox="0 0 24 24"
								stroke="currentColor"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
								/>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
								/>
							</svg>
						</div>
						<span class="text-gray-500 text-sm"
							>Baranya megye, Dél-Dunántúl</span
						>
					</li>
				</ul>
			</div>
		</div>

		<!-- Bottom bar -->
		<div
			class="border-t border-[#1e1e1e] pt-6 flex flex-col sm:flex-row items-center justify-between gap-3"
		>
			<p class="text-gray-700 text-xs">
				© {year} Pannon Laser Clean. Minden jog fenntartva.
			</p>
			<div class="flex items-center gap-1">
				<span
					class="w-1.5 h-1.5 rounded-full bg-orange-500 animate-pulse"
				></span>
				<span class="text-gray-700 text-xs"
					>Baranya megye · Dél-Dunántúl</span
				>
			</div>
		</div>
	</div>
</footer>
