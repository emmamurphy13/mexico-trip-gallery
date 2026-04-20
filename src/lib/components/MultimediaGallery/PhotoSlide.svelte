<!--
@component
PhotoSlide.svelte — A full-bleed photo slide with a gradient caption overlay.

Renders an image that fills the viewport with object-fit: cover. A gradient
overlay at the bottom displays the title, caption, and photo credit.

USAGE EXAMPLE:
<PhotoSlide photo={{
  filename: 'subway-platform.jpg',
  title: 'Waiting for the L',
  caption: 'Commuters line the platform at Bedford Avenue during morning rush.',
  credit: 'Photo by Jane Doe'
}} />
-->
<script>
  import { base } from '$app/paths';

  let {
    photo, // Object with filename, title, caption, and credit
  } = $props();
</script>

<div
  class="slide"
  class:right-photo={photo?.imageSide === 'right'}
  class:center-box={photo?.captionStyle === 'center-box'}
  class:full-bleed={photo?.captionStyle === 'full-bleed'}
  class:banner-box={photo?.captionStyle === 'banner-box'}
  class:split-panel={photo?.captionStyle === 'split-panel'}
  class:window-box={photo?.captionStyle === 'window-box'}
  data-slide
  data-photo
>
  <img src="{base}/photos/{photo.filename}" alt={photo.title} />
  <div class="caption">
    <div class="caption-inner">
      {#if photo.title}
        <h2>{photo.title}</h2>
      {/if}
      <p>{photo.caption}</p>
      {#if photo.credit}
        <span class="credit">{photo.credit}</span>
      {/if}
    </div>
  </div>
</div>

<style lang="scss">
  .slide {
    height: 100%;
    flex: 0 0 100%;
    position: relative;
    background: black;

    @container (min-width: 768px) {
      display: flex;
    }
  }

  .slide::before,
  .slide::after {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    height: 10px;
    z-index: 7;
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

  .slide.right-photo {
    @container (min-width: 768px) {
      flex-direction: row-reverse;
    }
  }

  .slide.center-box .caption {
    @container (min-width: 768px) {
      position: absolute;
      inset: 0;
      width: auto;
      background: transparent;
      padding: 2rem;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  }

  .slide.center-box .caption-inner {
    max-width: 40rem;
    background: rgba(0, 0, 0, 0.82);
    padding: 1rem 1.125rem;
    border-radius: 4px;
    text-align: center;

    @container (min-width: 768px) {
      padding: 1.5rem 1.75rem;
    }
  }

  .slide.center-box .caption p {
    margin: 0;
  }

  .slide.banner-box {
    @container (min-width: 768px) {
      display: block;
    }
  }

  .slide.banner-box img {
    @container (min-width: 768px) {
      width: 100%;
      height: 100%;
    }
  }

  .slide.banner-box .caption {
    @container (min-width: 768px) {
      position: absolute;
      inset: auto 0 12%;
      width: auto;
      background: transparent;
      padding: 0 1.5rem;
      display: flex;
      justify-content: center;
    }
  }

  .slide.banner-box .caption-inner {
    max-width: 42rem;
    width: 100%;
    background: rgba(0, 0, 0, 0.9);
    padding: 1rem 1.25rem;
    border-radius: 2px;
    text-align: center;

    @container (min-width: 768px) {
      padding: 1.25rem 1.75rem;
    }
  }

  .slide.banner-box .caption h2 {
    margin-bottom: 0.75rem;
  }

  .slide.banner-box .caption p {
    margin: 0;
  }

  .slide.banner-box .caption .credit {
    display: block;
    margin-top: 0.75rem;
  }

  .slide.split-panel {
    @container (min-width: 768px) {
      display: flex;
    }
  }

  .slide.split-panel img {
    @container (min-width: 768px) {
      width: 64%;
      flex-shrink: 0;
      object-position: center;
    }
  }

  .slide.split-panel .caption {
    @container (min-width: 768px) {
      position: static;
      width: 36%;
      min-width: 16rem;
      background: #050505;
      display: flex;
      align-items: center;
      padding: 2rem 1.5rem;
    }
  }

  .slide.split-panel .caption-inner {
    max-width: none;
    width: 100%;
    background: transparent;
    padding: 0;
  }

  .slide.split-panel .caption h2 {
    font-size: 1.1rem;
    letter-spacing: 0.02em;
    text-transform: uppercase;
  }

  .slide.split-panel .caption p {
    margin: 0;
    font-size: 1rem;
    line-height: 1.65;
    opacity: 1;
  }

  .slide.split-panel .caption .credit {
    display: block;
    margin-top: 1rem;
    opacity: 0.65;
  }

  .slide.window-box {
    @container (min-width: 768px) {
      display: block;
    }
  }

  .slide.window-box img {
    @container (min-width: 768px) {
      width: 100%;
      height: 100%;
    }
  }

  .slide.window-box .caption {
    @container (min-width: 768px) {
      position: absolute;
      left: 50%;
      bottom: 1.5rem;
      transform: translateX(-50%);
      width: min(84%, 40rem);
      background: transparent;
      padding: 0;
      display: flex;
      justify-content: center;
    }
  }

  .slide.window-box .caption-inner {
    width: 100%;
    background: rgba(0, 0, 0, 0.9);
    padding: 1rem 1.25rem;
    border-radius: 999px;
    text-align: center;

    @container (min-width: 768px) {
      padding: 1.1rem 1.75rem;
    }
  }

  .slide.window-box .caption h2 {
    margin-bottom: 0.4rem;
  }

  .slide.window-box .caption p {
    margin: 0;
  }

  .slide.window-box .caption .credit {
    display: block;
    margin-top: 0.6rem;
  }

  .slide.center-box img {
    @container (min-width: 768px) {
      width: 100%;
    }
  }

  .slide.full-bleed img {
    @container (min-width: 768px) {
      width: 100%;
    }
  }

  .slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;

    @container (min-width: 768px) {
      width: 60%;
      flex-shrink: 0;
    }
  }

  .caption {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 2rem 1.5rem 3.5rem;
    background: linear-gradient(
      to top,
      rgba(0, 0, 0, 0.85) 0%,
      rgba(0, 0, 0, 0.4) 70%,
      transparent 100%
    );
    color: white;

    @container (min-width: 768px) {
      position: static;
      width: 40%;
      background: black;
      display: flex;
      align-items: center;
      padding: 3rem;
    }
  }

  .slide.full-bleed .caption {
    @container (min-width: 768px) {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      width: auto;
      background: linear-gradient(
        to top,
        rgba(0, 0, 0, 0.85) 0%,
        rgba(0, 0, 0, 0.4) 70%,
        transparent 100%
      );
      padding: 2rem 1.5rem 3.5rem;
    }
  }

  .caption-inner {
    max-width: 600px;
    border-inline-start: 4px solid #006847;
    border-inline-end: 4px solid #ce1126;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.28);
  }

  .caption h2 {
    margin: 0 0 0.5rem;
    font-size: 1.25rem;
    line-height: 1.3;
    color: white;

    @container (min-width: 768px) {
      font-size: 1.75rem;
      margin-bottom: 1rem;
    }
  }

  .caption p {
    margin: 0 0 0.5rem;
    font-size: 0.9375rem;
    line-height: 1.5;
    opacity: 0.9;

    @container (min-width: 768px) {
      font-size: 1.0625rem;
      line-height: 1.7;
      margin-bottom: 1.5rem;
    }
  }

  .caption .credit {
    font-size: 0.75rem;
    opacity: 0.6;

    @container (min-width: 768px) {
      font-size: 0.8125rem;
    }
  }
</style>
