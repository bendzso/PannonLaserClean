<script lang="ts">
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;

	onMount(() => {
		const ctx = canvas.getContext('2d')!;
		let raf: number;
		let w = 0, h = 0;

		const lines = [
			{ y: 0.12, speed: 0.5,  color: '#f97316', scanX: 0 },
			{ y: 0.27, speed: 0.3,  color: '#3b82f6', scanX: 600 },
			{ y: 0.43, speed: 0.65, color: '#f97316', scanX: 200 },
			{ y: 0.58, speed: 0.38, color: '#3b82f6', scanX: 900 },
			{ y: 0.72, speed: 0.55, color: '#f97316', scanX: 400 },
			{ y: 0.88, speed: 0.25, color: '#3b82f6', scanX: 1100 },
		];

		function resize() {
			w = canvas.width = window.innerWidth;
			h = canvas.height = window.innerHeight;
		}

		function hexToRgb(hex: string) {
			const r = parseInt(hex.slice(1, 3), 16);
			const g = parseInt(hex.slice(3, 5), 16);
			const b = parseInt(hex.slice(5, 7), 16);
			return `${r},${g},${b}`;
		}

		function draw() {
			ctx.clearRect(0, 0, w, h);

			for (const line of lines) {
				const y = line.y * h;
				const rgb = hexToRgb(line.color);

				// Full-width faint base line
				ctx.save();
				ctx.strokeStyle = `rgba(${rgb}, 0.06)`;
				ctx.lineWidth = 1;
				ctx.beginPath();
				ctx.moveTo(0, y);
				ctx.lineTo(w, y);
				ctx.stroke();
				ctx.restore();

				// Moving scanner beam
				line.scanX = (line.scanX + line.speed) % (w + 500);
				const sx = line.scanX - 250;
				const beamWidth = 260;

				const glow = ctx.createLinearGradient(sx, 0, sx + beamWidth, 0);
				glow.addColorStop(0,    `rgba(${rgb}, 0)`);
				glow.addColorStop(0.25, `rgba(${rgb}, 0.25)`);
				glow.addColorStop(0.55, `rgba(${rgb}, 0.9)`);
				glow.addColorStop(0.75, `rgba(${rgb}, 0.5)`);
				glow.addColorStop(1,    `rgba(${rgb}, 0)`);

				ctx.save();
				ctx.shadowColor = line.color;
				ctx.shadowBlur = 18;
				ctx.strokeStyle = glow;
				ctx.lineWidth = 2;
				ctx.beginPath();
				ctx.moveTo(sx, y);
				ctx.lineTo(sx + beamWidth, y);
				ctx.stroke();

				// second pass for extra glow intensity
				ctx.shadowBlur = 6;
				ctx.lineWidth = 1;
				ctx.stroke();
				ctx.restore();
			}

			raf = requestAnimationFrame(draw);
		}

		resize();
		window.addEventListener('resize', resize);
		draw();

		return () => {
			cancelAnimationFrame(raf);
			window.removeEventListener('resize', resize);
		};
	});
</script>

<canvas
	bind:this={canvas}
	class="fixed inset-0 w-full h-full pointer-events-none"
	style="z-index: 10; mix-blend-mode: screen;"
></canvas>
