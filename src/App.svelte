<script>
  import { fly, fade, scale, slide } from 'svelte/transition';
  import { cubicOut } from 'svelte/easing';
  import { onMount } from 'svelte';
  import { tick } from 'svelte';

  let slogans = [
    "We don’t follow industry standards—we set them.",
    "Good enough isn’t good enough. We build security that lasts.",
    "We don’t wait for problems. We eliminate them before they exist.",
    "What others call ‘advanced,’ we call ‘standard.’",
    "Security isn’t about reacting. It’s about always being ahead.",
    "We don’t cut corners. We reinforce them.",
    "Built with cutting-edge tech. Designed to never need an update.",
    "When the rest of the world is in the dark, your security is still running.",
    "The grid fails. Our systems don’t.",
    "Security that doesn’t just protect—it adapts, outsmarts, and evolves."
  ];

  let current = 0;
  let transitions = [fade, fly, scale, slide];
  let transitionIndex = 0;
  let slogan;

  onMount(async () => {
    while (true) {
      slogan = slogans[current];
      transitionIndex = (transitionIndex + 1) % transitions.length;
      await tick();
      await new Promise(r => setTimeout(r, 4000));
      current = (current + 1) % slogans.length;
    }
  });
</script>

<style>
  .hero {
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: radial-gradient(circle, #0f0f0f, #1a1a1a);
    color: #fff;
    font-size: 2.5rem;
    font-weight: 700;
    text-align: center;
    padding: 2rem;
    overflow: hidden;
  }
</style>

<div class="hero">
  {#key slogan}
    <div transition:{transitions[transitionIndex]}={{ duration: 800, easing: cubicOut }}>
      {slogan}
    </div>
  {/key}
</div>
