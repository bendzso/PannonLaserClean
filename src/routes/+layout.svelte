<script lang="ts">
	import '../app.css';

	let { children } = $props();
</script>

<svelte:head>
	<title>Pannon Laser Clean – Lézeres tisztítás Baranyában</title>
	<meta name="description" content="Professzionális, érintésmentes lézeres tisztítás fém, fa és ipari felületeken. Mobil szolgáltatás a Dél-Dunántúlon." />
	<meta name="viewport" content="width=device-width, initial-scale=1" />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet" />
</svelte:head>

{@render children()}
