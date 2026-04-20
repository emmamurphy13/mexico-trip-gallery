<script>
  import SlideGallery from '$lib/components/MultimediaGallery/SlideGallery.svelte';
  import TitleSlide from '$lib/components/MultimediaGallery/TitleSlide.svelte';
  import PhotoSlide from '$lib/components/MultimediaGallery/PhotoSlide.svelte';
  import DoublePhotoSlide from '$lib/components/MultimediaGallery/DoublePhotoSlide.svelte';
  import TextSlide from '$lib/components/MultimediaGallery/TextSlide.svelte';
  import CreditsSlide from '$lib/components/MultimediaGallery/CreditsSlide.svelte';

  let { data } = $props();
</script>

<svelte:head>
  <title>Mexico Trip Gallery</title>
  <meta name="description" content="A full-screen multimedia photo story." />
</svelte:head>

<SlideGallery>
  <TitleSlide
    headline="Mexico Trip Gallery"
    intro="On Spring Break five journalist friends take a trip to two mexican cities."
    byline="By Emma Murphy"
    backgroundFilename="jpegmini_optimized-2/1.jpg"
  />

  {#each data.story as slide (slide.id)}
    {#if slide.type === 'photo'}
      <PhotoSlide photo={slide} />
    {:else if slide.type === 'double-photo'}
      <DoublePhotoSlide {slide} />
    {:else if slide.type === 'text'}
      <TextSlide {slide} />
    {/if}
  {/each}

  <CreditsSlide>
    <h2>Credits</h2>
    <p>
      Photography and captions by Emma Murphy.
    </p>
  </CreditsSlide>
</SlideGallery>
