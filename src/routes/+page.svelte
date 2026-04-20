<script lang="ts">
	import LaserBackground from '$lib/components/LaserBackground.svelte';
	import Nav from '$lib/components/Nav.svelte';
	import Hero from '$lib/components/Hero.svelte';
	import About from '$lib/components/About.svelte';
	import Services from '$lib/components/Services.svelte';
	import WhyLaser from '$lib/components/WhyLaser.svelte';
	import HowWeWork from '$lib/components/HowWeWork.svelte';
	import Gallery from '$lib/components/Gallery.svelte';
	import BeforeAfter from '$lib/components/BeforeAfter.svelte';
	import FAQ from '$lib/components/FAQ.svelte';
	import TrustBlock from '$lib/components/TrustBlock.svelte';
	import ContactForm from '$lib/components/ContactForm.svelte';
	import Footer from '$lib/components/Footer.svelte';
</script>

<div class="relative min-h-screen">
	<LaserBackground />

	<div class="relative" style="z-index: 2;">
		<Nav />
		<main>
			<Hero />
			<About />
			<Services />
			<WhyLaser />
			<HowWeWork />
			<Gallery />
			<BeforeAfter />
			<FAQ />
			<TrustBlock />
			<ContactForm />
		</main>
		<Footer />
	</div>
</div>
