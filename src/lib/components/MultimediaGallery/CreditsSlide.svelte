<!--
@component
CreditsSlide.svelte — A closing credits slide rendered via a children snippet.

Provides a flexible container for credits, acknowledgments, or any closing
content at the end of a multimedia gallery.

USAGE EXAMPLE:
<CreditsSlide>
  <h2>Credits</h2>
  <p>Photography by Jane Doe</p>
  <p>Text by John Smith</p>
</CreditsSlide>
-->
<script>
  let {
    children, // Content rendered inside the credits slide
  } = $props();
</script>

<div class="slide" data-slide>
  <div class="content">
    {@render children()}
  </div>
</div>

<style>
  .slide {
    height: 100%;
    flex: 0 0 100%;
    background:
      radial-gradient(circle at 16% 20%, rgba(0, 104, 71, 0.24), transparent 38%),
      radial-gradient(circle at 84% 76%, rgba(206, 17, 38, 0.2), transparent 40%),
      linear-gradient(160deg, #1f140f 0%, #120d0b 55%, #1e0d12 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
  }

  .slide::before,
  .slide::after {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    height: 10px;
    background: repeating-linear-gradient(
      90deg,
      #006847 0 24px,
      #f6efe2 24px 48px,
      #ce1126 48px 72px
    );
  }

  .slide::before {
    top: 0;
  }

  .slide::after {
    bottom: 0;
  }

  .content {
    max-width: 600px;
    padding: 2rem;
    color: white;
    background: rgba(8, 8, 8, 0.82);
    border-radius: 6px;
    border-left: 4px solid #006847;
    border-right: 4px solid #ce1126;
    box-shadow: 0 10px 28px rgba(0, 0, 0, 0.35);
  }

  .content :global(h2) {
    font-size: 1.5rem;
    margin: 0 0 1rem;
    color: white;
  }

  .content :global(p) {
    font-size: 0.9375rem;
    line-height: 1.6;
    opacity: 0.85;
    margin: 0 0 1rem;
  }

  .content :global(a) {
    color: white;
    opacity: 0.7;
  }

  .content :global(a:hover),
  .content :global(a:focus-visible) {
    opacity: 1;
  }

  .content :global(a:focus-visible) {
    outline: 2px solid var(--color-white);
    outline-offset: 2px;
  }
</style>
