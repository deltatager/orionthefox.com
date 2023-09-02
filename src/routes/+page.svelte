<script>
  import Qr from './Qr.svelte'
  import sticker from '../lib/images/orion.png'
</script>

<svelte:head>
  <title>Orion 🌌🦊</title>
  <meta name="viewport" content="initial-scale=1, height=device-height, width=device-width" />
  <meta name="description" content="Orion's social media links" />
  <meta name="thumbnail" content="https://orionthefox.com/_app/immutable/assets/orion.d94da32f.png" />
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:image:src" content="https://orionthefox.com/_app/immutable/assets/orion.d94da32f.png" />
</svelte:head>

<section class="img-link">
  <img src={sticker} alt="Orion wink" width="300" />
  <a href="https://twitter.com/WeaselDumb" target="_blank">
    <span class="img-credit">by @WeaselDumb</span>
  </a>
</section>
<h1>Orion the Astrology fox</h1>
<section>
  <Qr
    data={'https://t.me/orionthefox'}
    label={'Telegram: @orionthefox'}
    image={'https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Telegram_logo.svg/128px-Telegram_logo.svg.png'}
    dotsOptions={{
      type: 'rounded',
      color: '#289fd9'
    }}
  />
  <Qr
    data={'https://www.instagram.com/orion.the.astro.fox'}
    label={'Instagram: @orion.the.astro.fox'}
    image={'https://upload.wikimedia.org/wikipedia/commons/e/e7/Instagram_logo_2016.svg'}
    dotsOptions={{
      type: 'dots',
      gradient: {
        type: 'linear',
        rotation: -45,
        colorStops: [
          {
            offset: 0,
            color: '#fb5'
          },
          {
            offset: 0.1,
            color: '#fb5'
          },
          {
            offset: 0.5,
            color: '#ff543e'
          },
          {
            offset: 1,
            color: '#c837ab'
          }
        ]
      }
    }}
  />
  <Qr
    data={'https://twitter.com/orionthefox'}
    label={'Twitter: @orionthefox'}
    image={'https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Logo_of_Twitter.svg/292px-Logo_of_Twitter.svg.png'}
    dotsOptions={{
      type: 'rounded',
      color: '#1d9bf0'
    }}
  />
</section>

<style>
  h1 {
    background: -webkit-linear-gradient(white, #38495a);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  img {
    display: block;
    filter: drop-shadow(0 0 3px #fff);
  }

  * {
    text-align: center;
  }

  section {
    display: flex;
    justify-content: center;
    align-items: center;
    flex: 0.7;
  }

  .img-link {
    text-align: left;
    flex-direction: column;
  }

  .img-link a {
    position: relative;
    left: -60px;
  }

  .img-credit {
    padding-left: 45px;
  }

  @media (max-width: 960px) {
    section {
      flex-direction: column;
    }
  }
</style>
