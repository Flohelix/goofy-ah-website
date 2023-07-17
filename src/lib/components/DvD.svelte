<script lang="ts">
  import { onMount, tick } from 'svelte';

  let dvd: HTMLImageElement;
  let container: HTMLDivElement;

  let dvdRect: any;
  let containerRect: any;

  let dx = 2;
  let dy = 2;

  const moveDVD = () => {
    if (dvdRect === undefined || containerRect === undefined) return;
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
  };

  onMount(async () => {
    await tick();
    dvdRect = dvd.getBoundingClientRect();
    containerRect = container.getBoundingClientRect();

    setInterval(moveDVD, 20);
  });
</script>

<img
  class="absolute z-40"
  src="goofy.webp"
  alt="Goofy dvd Logo"
  bind:this={dvd}
/>
<div class="h-screen w-screen absolute top-0 left-0 overflow-hidden" bind:this={container} />
