<script lang="ts">
  import { onMount, tick } from 'svelte';

  let dvd: HTMLImageElement;
  let container: HTMLDivElement;

  let dvdRect: any;
  let containerRect: any;

  let dx = 2;
  let dy = 2;

  let lastTime = 0;
  const fpsInterval = 1000 / 40; // duration between frames for 20 FPS

  const moveDVD = (timestamp: number) => {
    if (dvdRect === undefined || containerRect === undefined) return;

    // Calculate the elapsed time since the last frame
    const elapsedTime = timestamp - lastTime;

    // Check if the time since the last frame is greater than our interval
    if (elapsedTime > fpsInterval) {
      dvdRect = dvd.getBoundingClientRect();
      containerRect = container.getBoundingClientRect();

      if (
        dvdRect.left < containerRect.left ||
        dvdRect.right > containerRect.right
      ) {
        dx = -dx;
      }

      if (
        dvdRect.top < containerRect.top ||
        dvdRect.bottom > containerRect.bottom
      ) {
        dy = -dy;
      }

      dvd.style.left = `${dvd.offsetLeft + dx}px`;
      dvd.style.top = `${dvd.offsetTop + dy}px`;

      // Save the timestamp
      lastTime = timestamp;
    }

    requestAnimationFrame(moveDVD);
  };

  onMount(async () => {
    await tick();
    dvdRect = dvd.getBoundingClientRect();
    containerRect = container.getBoundingClientRect();

    requestAnimationFrame(moveDVD);
  });
</script>

<img
  class="absolute z-40 overflow-hidden"
  src="goofy.webp"
  alt="Goofy dvd Logo"
  bind:this={dvd}
/>
<div
  class="h-screen w-screen absolute top-0 left-0 overflow-hidden"
  bind:this={container}
/>
