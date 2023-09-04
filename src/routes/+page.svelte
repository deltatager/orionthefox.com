<script>
  import sticker from '../lib/images/orion.png'
  import QrCodes from './QrCodes.svelte'

  const title = 'Orion 🌌🦊'
  const description = "Orion's social media links"
  const imageSrc = 'https://orionthefox.com/_app/immutable/assets/orion.d94da32f.png'
</script>

<svelte:head>
  <title>{title}</title>
  <meta name="viewport" content="initial-scale=1, height=device-height, width=device-width" />
  <meta name="description" content={description} />
  <meta name="thumbnail" content={imageSrc} />

  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
  <meta property="og:type" content="article" />
  <meta property="og:url" content="https://orionthefox.com/" />
  <meta property="og:image" content={imageSrc} />
  <meta property="og:image:type" content="image/png" />
  <meta property="og:image:width" content="430" />
  <meta property="og:image:height" content="506" />

  <meta name="twitter:site" content={title} />
  <meta name="twitter:title" content={title} />
  <meta name="twitter:description" content={description} />
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:image:src" content={imageSrc} />
  <meta name="theme-color" content="#3198AB" />
</svelte:head>

<section>
  <img src={sticker} alt="Orion wink" width="300" />
  <a href="https://twitter.com/WeaselDumb" target="_blank">
    <span>by @WeaselDumb</span>
  </a>
</section>

<h1>Orion the Astrology fox</h1>

<QrCodes />

<style>
  h1 {
    background: linear-gradient(white, #38495a);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  img {
    filter: drop-shadow(0 0 3px #fff);
  }

  section {
    display: flex;
    align-items: center;
    flex-direction: column;
  }

  section a {
    position: relative;
    left: -45px;
  }
</style>
