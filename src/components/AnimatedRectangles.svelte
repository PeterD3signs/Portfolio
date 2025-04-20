<script lang="ts">
  import { onMount } from 'svelte';

  let canvas: HTMLCanvasElement;
  let ctx: CanvasRenderingContext2D;

  export let rectSize = 50; //Set rectangle size
  export let baseColor = [237, 196, 62]; // Set rectangle color

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
        const dx = mouseX - (x + rectSize / 2); // Distance form the center of the rectangle to the mouse on the X axis
        const dy = mouseY - (y + rectSize / 2); // Distance form the center of the rectangle to the mouse on the Y axis
        const dist = Math.sqrt(dx * dx + dy * dy);  // Absolute distance calculated from the Pythagorean theorem
        const maxDist = Math.sqrt(width * width + height * height); // Maximum possible disctance
        const norm = dist / maxDist;  // Normalized distance between 0 and 1
        const brightness = 0.7 * (1 - Math.pow(norm, 0.3)); // Brightness based on distance from the mouse (0.7 factor sleected by trial and error)
        ctx.fillStyle = `rgba(${baseColor.join(',')}, ${brightness})`;  // Connect base color with alpha
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
