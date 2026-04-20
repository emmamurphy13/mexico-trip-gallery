<script>
  import { base } from '$app/paths';

  let {
    slide, // Object with leftFilename, rightFilename and caption
  } = $props();
</script>

<div class="slide" data-slide data-photo data-double-photo>
  <div class="images">
    <img src="{base}/photos/{slide.leftFilename}" alt={slide.leftAlt || ''} />
    <div class="divider" aria-hidden="true">
      <div class="divider-inner">
        <p>{slide.caption}</p>
      </div>
    </div>
    <img src="{base}/photos/{slide.rightFilename}" alt={slide.rightAlt || ''} />
  </div>
</div>

<style>
  .slide {
    height: 100%;
    flex: 0 0 100%;
    position: relative;
    background: #050505;
  }

  .slide::before,
  .slide::after {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    height: 10px;
    z-index: 5;
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

  .images {
    display: grid;
    grid-template-columns: 1fr minmax(11rem, 18rem) 1fr;
    height: 100%;
    gap: 0;
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }

  .images > img {
    min-width: 0;
    object-position: center;
  }

  .divider {
    background: linear-gradient(180deg, #101010 0%, #000 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1rem;
    z-index: 2;
  }

  .divider-inner {
    width: 100%;
    max-width: 15rem;
  }

  .divider p {
    margin: 0;
    color: white;
    text-align: center;
    line-height: 1.55;
    font-size: 0.95rem;
    background: transparent;
    padding: 0;
    border-left: 3px solid #006847;
    border-right: 3px solid #ce1126;
    padding-left: 0.85rem;
    padding-right: 0.85rem;
  }

  @container (min-width: 768px) {
    .images {
      grid-template-columns: 1fr minmax(14rem, 22rem) 1fr;
    }

    .divider {
      padding: 1.5rem 1.25rem;
    }

    .divider-inner {
      max-width: 18rem;
    }

    .divider p {
      font-size: 1.05rem;
    }
  }
</style>
