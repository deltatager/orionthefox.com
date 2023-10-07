<script lang="ts">
  import QrCodes from './QrCodes.svelte'
  import sticker0 from '../lib/images/stickers/0.png'
  import sticker1 from '../lib/images/stickers/1.png'
  import sticker2 from '../lib/images/stickers/2.png'
  import sticker3 from '../lib/images/stickers/3.png'
  import sticker4 from '../lib/images/stickers/4.png'

  const stickers = [
    {
      src: sticker0,
      artist: 'WeaselDumb'
    },
    {
      src: sticker1,
      artist: 'SpaceFoxJupiter'
    },
    {
      src: sticker2,
      artist: 'SpaceFoxJupiter'
    },
    {
      src: sticker3,
      artist: 'SpaceFoxJupiter'
    },
    {
      src: sticker4,
      artist: 'Wren_Petrova'
    }
  ]

  const { src, artist } = stickers[Math.round(Math.random() * stickers.length)]

  const title = 'Orion 🌌🦊'
  const description = "Orion's social media links"
</script>

<svelte:head>
  <title>{title}</title>
  <meta name="viewport" content="initial-scale=1, height=device-height, width=device-width" />
  <meta name="description" content={description} />
  <meta name="thumbnail" content={src} />

  <meta property="og:title" content={title} />
  <meta property="og:description" content={description} />
  <meta property="og:type" content="article" />
  <meta property="og:url" content="https://orionthefox.com/" />
  <meta property="og:image" content={src} />
  <meta property="og:image:type" content="image/png" />
  <meta property="og:image:width" content="430" />
  <meta property="og:image:height" content="506" />

  <meta name="twitter:site" content={title} />
  <meta name="twitter:title" content={title} />
  <meta name="twitter:description" content={description} />
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:image:src" content={src} />
  <meta name="theme-color" content="#3198AB" />
</svelte:head>

<section>
  <img {src} alt="Orion sticker" width="300" />
  <a href={`https://twitter.com/${artist}`} target="_blank">
    <span>by @{artist}</span>
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
