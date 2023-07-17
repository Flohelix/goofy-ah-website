<script lang="ts">
  import Goofy from '$lib/components/Goofy.svelte';
  import DvD from '$lib/components/DvD.svelte';

</script>

<Goofy />
<DvD />

<div
  class="flex justify-center items-center flex-col h-screen w-screen bg-[#0e0e10] gap-4"
>
  <div class="p-5 bg-[#1f1f23] rounded-xl relative z-20">
    <div class="relative z-20 text-5xl text-white font-bold gradient-text">
      LATTENCOCK.DE
    </div>
  </div>
  <div class="flex justify-center items-center">
    <div class="relative z-20">
      <iframe
        src="https://player.twitch.tv/?channel=papaplatte&parent=localhost"
        height="630"
        width="1120"
        allowfullscreen
        title="Papaplatte Twitch Player"
      />
    </div>
    <div class="relative z-20">
      <iframe
        src="https://www.twitch.tv/embed/papaplatte/chat?darkpopout&parent=localhost"
        height="630"
        width="400"
        title="Papaplatte Twitch Chat"
      />
    </div>
  </div>
</div>

<style>
  @keyframes gradient-animation {
    0% {
      background-position: 0%;
    }
    50% {
      background-position: 100%;
    }
    100% {
      background-position: 0%;
    }
  }

  .gradient-text {
    background: linear-gradient(270deg, red, blue, red);
    background-size: 200%;
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    font-size: 48px;
    animation: gradient-animation 5s linear infinite;
  }
</style>
