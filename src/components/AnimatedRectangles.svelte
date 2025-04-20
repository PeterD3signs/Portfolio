<script lang="ts">
  import { onMount } from 'svelte';

  let canvas: HTMLCanvasElement;
  let ctx: CanvasRenderingContext2D;

  export let rectSize = 50;
  export let baseColor = [237, 196, 62]; // RGB array

  let width = 0;
  let height = 0;
  let mouseX = 0;
  let mouseY = 0;

  function resizeCanvas() {
    width = window.innerWidth;
    height = window.innerHeight;
    canvas.width = width;
    canvas.height = height;
  }

  function draw() {
    ctx.clearRect(0, 0, width, height);

    for (let y = 0; y < height; y += rectSize) {
      for (let x = 0; x < width; x += rectSize) {
        const dx = mouseX - (x + rectSize / 2);
        const dy = mouseY - (y + rectSize / 2);
        const dist = Math.sqrt(dx * dx + dy * dy);
        const maxDist = Math.sqrt(width * width + height * height);
        const norm = dist / maxDist;
        const brightness = 0.7 * (1 - Math.pow(norm, 0.3));
        ctx.fillStyle = `rgba(${baseColor.join(',')}, ${brightness})`;
        ctx.fillRect(x, y, rectSize, rectSize);
      }
    }
  }

  function animate() {
    draw();
    requestAnimationFrame(animate);
  }

  function handleMouseMove(e: MouseEvent) {
    mouseX = e.clientX;
    mouseY = e.clientY;
  }

  onMount(() => {
    ctx = canvas.getContext('2d')!;
    resizeCanvas();
    window.addEventListener('resize', resizeCanvas);
    window.addEventListener('mousemove', handleMouseMove);
    animate();

    return () => {
      window.removeEventListener('resize', resizeCanvas);
      window.removeEventListener('mousemove', handleMouseMove);
    };
  });
</script>

<canvas
  bind:this={canvas}
  class="fixed top-0 left-0 w-full h-full z-[-10] pointer-events-none"
></canvas>
