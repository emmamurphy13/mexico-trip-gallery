<!--
@component
TitleSlide.svelte — The opening slide of a multimedia gallery.

Displays a centered headline, introductory text, byline, and a
"Scroll to begin" hint on a full-screen black background.

USAGE EXAMPLE:
<TitleSlide
  headline="Life on the L Train"
  intro="A photo essay documenting commuters on New York's busiest crosstown line."
  byline="By Jane Doe"
/>
-->
<script>
  import { base } from '$app/paths';

  let {
    headline, // The main gallery title
    intro, // Introductory text below the headline
    byline, // Author attribution
    backgroundFilename = null, // Optional background photo filename from /static/photos
  } = $props();
</script>

<div
  class="slide"
  data-slide
  style={backgroundFilename
    ? `background-image: linear-gradient(rgba(0,0,0,.55), rgba(0,0,0,.65)), url('${base}/photos/${backgroundFilename}')`
    : undefined}
>
  <div class="masthead">
    <a
      href="https://www.nycitynewsservice.com/"
      class="logo"
      aria-label="NYCity News Service"
    >
      <span class="logo-text">
        <span class="logo-nycity">NYCITY</span><span class="logo-news-service"
          >News Service</span
        >
      </span>
    </a>
  </div>
  <div class="content">
    <h1>{headline}</h1>
    <p class="intro">{intro}</p>
    <p class="byline">{byline}</p>
  </div>
  <div class="scroll-hint">Tap to begin →</div>
</div>

<style lang="scss">
  @use '../../styles' as *;

  .slide {
    height: 100%;
    flex: 0 0 100%;
    background-color: black;
    background-size: cover;
    background-position: center;
    display: flex;
    flex-direction: column;
    position: relative;
  }

  .slide::before,
  .slide::after {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    height: 10px;
    z-index: 6;
    pointer-events: none;
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

  .masthead {
    display: flex;
    justify-content: center;
    padding: var(--spacing-xs) var(--spacing-sm);
    background: linear-gradient(
      90deg,
      #005c3d 0%,
      #0f7a51 30%,
      #f7f1e8 52%,
      #b71c2d 76%,
      #8f1121 100%
    );
    background-size: 200% 100%;
    animation: gradient-sweep 6s ease-in-out infinite;
  }

  @keyframes gradient-sweep {
    0% {
      background-position: 0% 0%;
    }
    50% {
      background-position: 100% 0%;
    }
    100% {
      background-position: 0% 0%;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .masthead {
      animation: none;
    }
  }

  .logo {
    display: inline-block;
    text-decoration: none;
  }

  .logo:hover {
    text-decoration: none;
  }

  .logo:focus-visible {
    outline: 2px solid var(--color-white);
    outline-offset: 2px;
  }

  .logo-text {
    display: inline-flex;
    align-items: stretch;
    border: 1px solid var(--color-white);
  }

  .logo-nycity {
    background-color: var(--color-white);
    color: var(--color-accent);
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: var(--font-weight-extrabold);
    padding: var(--logo-padding-mobile);
    letter-spacing: var(--letter-spacing-wide);
    text-transform: uppercase;
    display: flex;
    align-items: center;
  }

  .logo-news-service {
    color: var(--color-white);
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: var(--font-weight-light);
    padding: var(--logo-padding-mobile);
    letter-spacing: var(--letter-spacing-tight);
    display: flex;
    align-items: center;
  }

  .content {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    max-width: 600px;
    margin: 0 auto;
    padding: 2rem;
    color: white;
    text-align: center;
    background: linear-gradient(
      180deg,
      rgba(0, 0, 0, 0.42) 0%,
      rgba(0, 0, 0, 0.64) 100%
    );
    border-top: 3px solid rgba(0, 104, 71, 0.72);
    border-bottom: 3px solid rgba(206, 17, 38, 0.72);
  }

  h1 {
    font-size: 2rem;
    line-height: 1.2;
    margin: 0 0 1rem;
    color: white;

    @container (min-width: 768px) {
      font-size: 3.5rem;
    }
  }

  .intro {
    font-size: 1.0625rem;
    line-height: 1.6;
    opacity: 0.85;
    margin: 0 0 1.5rem;

    @container (min-width: 768px) {
      font-size: 1.375rem;
      line-height: 1.7;
    }
  }

  .byline {
    font-size: 0.875rem;
    opacity: 0.6;
    margin: 0;

    @container (min-width: 768px) {
      font-size: 1.125rem;
    }
  }

  .scroll-hint {
    font-size: 0.8125rem;
    opacity: 0.6;
    margin: 0;
    padding-bottom: 3.5rem;
    color: white;
    display: flex;
    justify-content: center;
  }
</style>
