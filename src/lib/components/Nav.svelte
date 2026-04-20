<script lang="ts">
	import { onMount } from "svelte";

	let scrolled = $state(false);
	let menuOpen = $state(false);

	const links = [
		{ label: "Szolgáltatások", href: "#szolgaltatasok" },
		{ label: "Miért lézer?", href: "#miert-lezer" },
		{ label: "Galéria", href: "#galeria" },
		{ label: "GYIK", href: "#gyik" },
	];

	onMount(() => {
		const onScroll = () => {
			scrolled = window.scrollY > 40;
		};
		window.addEventListener("scroll", onScroll, { passive: true });
		return () => window.removeEventListener("scroll", onScroll);
	});

	function close() {
		menuOpen = false;
	}
</script>

<nav
	class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
	class:bg-nav={scrolled}
>
	<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex items-center justify-between h-16 lg:h-20">
			<!-- Logo -->
			<a
				href="#hero"
				class="flex items-center gap-3 group"
				onclick={close}
			>
				<img
					src="/gallery/logo.png"
					alt="Pannon Laser Clean logó"
					class="h-18 w-auto rounded-lg"
				/>
			</a>

			<!-- Desktop links -->
			<div class="hidden lg:flex items-center gap-8">
				{#each links as link}
					<a
						href={link.href}
						class="text-gray-400 hover:text-white text-sm font-medium transition-colors duration-200 hover:text-orange-400"
					>
						{link.label}
					</a>
				{/each}
				<a href="#kapcsolat" class="btn-primary text-sm px-5 py-2.5">
					Ajánlatkérés
					<svg
						xmlns="http://www.w3.org/2000/svg"
						class="w-4 h-4"
						fill="none"
						viewBox="0 0 24 24"
						stroke="currentColor"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M17 8l4 4m0 0l-4 4m4-4H3"
						/>
					</svg>
				</a>
			</div>

			<!-- Mobile hamburger -->
			<button
				class="lg:hidden text-gray-400 hover:text-white p-2"
				onclick={() => (menuOpen = !menuOpen)}
				aria-label="Menü"
			>
				<div class="w-6 flex flex-col gap-1.5 transition-all">
					<span
						class="block h-0.5 bg-current transition-all duration-300"
						class:rotate-45={menuOpen}
						class:translate-y-2={menuOpen}
					></span>
					<span
						class="block h-0.5 bg-current transition-all duration-300"
						class:opacity-0={menuOpen}
					></span>
					<span
						class="block h-0.5 bg-current transition-all duration-300"
						class:-rotate-45={menuOpen}
						class:-translate-y-2={menuOpen}
					></span>
				</div>
			</button>
		</div>
	</div>

	<!-- Mobile menu -->
	{#if menuOpen}
		<div
			class="lg:hidden bg-[#111] border-t border-[#2a2a2a] px-4 py-4 flex flex-col gap-4"
		>
			{#each links as link}
				<a
					href={link.href}
					class="text-gray-300 text-base font-medium py-1"
					onclick={close}
				>
					{link.label}
				</a>
			{/each}
			<a
				href="#kapcsolat"
				class="btn-primary text-center mt-2"
				onclick={close}
			>
				Ajánlatkérés
			</a>
		</div>
	{/if}
</nav>

<style>
	.bg-nav {
		background: rgba(15, 15, 15, 0.95);
		backdrop-filter: blur(12px);
		border-bottom: 1px solid rgba(42, 42, 42, 0.8);
		box-shadow: 0 4px 24px rgba(0, 0, 0, 0.4);
	}
</style>
