<!--
@component
TextSlide.svelte — A centered text slide for narrative context between photos.

Displays a headline and body paragraph on a full-screen black background,
providing editorial context within a multimedia gallery sequence.

USAGE EXAMPLE:
<TextSlide slide={{
  headline: 'The Commute',
  body: 'Every day, thousands of riders depend on the L train to cross between Brooklyn and Manhattan.'
}} />
-->
<script>
  let {
    slide, // Object with headline and body text
  } = $props();
</script>

<div class="slide" data-slide>
  <div class="content">
    <h2>{slide.headline}</h2>
    <p>{slide.body}</p>
  </div>
</div>

<style>
  .slide {
    height: 100%;
    flex: 0 0 100%;
    background:
      radial-gradient(circle at 18% 22%, rgba(0, 104, 71, 0.25), transparent 40%),
      radial-gradient(circle at 80% 78%, rgba(206, 17, 38, 0.22), transparent 42%),
      linear-gradient(160deg, #2a160e 0%, #130d0a 58%, #250e13 100%);
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
    max-width: 560px;
    padding: 2rem;
    color: white;
    text-align: center;
    background: rgba(12, 10, 9, 0.8);
    border-radius: 6px;
    border-top: 4px solid #006847;
    border-bottom: 4px solid #ce1126;
    box-shadow: 0 10px 28px rgba(0, 0, 0, 0.35);
  }

  h2 {
    font-size: 1.75rem;
    line-height: 1.2;
    margin: 0 0 1rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: white;
  }

  p {
    font-size: 1.0625rem;
    line-height: 1.7;
    opacity: 0.8;
    margin: 0;
  }
</style>
