<script>
  import instagramQr from '$lib/images/instagram_qr.png'
  import welcome_fallback from '$lib/images/svelte-welcome.png'
  import welcome from '$lib/images/svelte-welcome.webp'
  import Qr from './Qr.svelte'
</script>

<svelte:head>
  <title>Home</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
  <h1>
    <span class="welcome">
      <picture>
        <source srcset={welcome} type="image/webp" />
        <img src={welcome_fallback} alt="Welcome" />
      </picture>
    </span>

    to your new<br />SvelteKit app
  </h1>

  <h2>
    try editing <strong>src/routes/+page.svelte</strong>
  </h2>

  <div class="cards">
    <Qr
      data={'https://t.me/orionthefox'}
      label={'Telegram: @orionthefox'}
      image={'https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Telegram_logo.svg/2048px-Telegram_logo.svg.png'}
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
          type: 'radial',
          rotation: 0,
          colorStops: [
            {
              offset: 0,
              color: '#fd5'
            },
            {
              offset: .1,
              color: '#fd5'
            },
            {
              offset: 0.5,
              color: '#ff543e'
            },
            {
              offset: 1,
              color: '#c837ab'
            },
          ]
        }
      }}
    />
  </div>
</section>

<style>
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex: 0.6;
  }

  h1 {
    width: 100%;
  }

  .welcome {
    display: block;
    position: relative;
    width: 100%;
    height: 0;
    padding: 0 0 calc(100% * 495 / 2048) 0;
  }

  .welcome img {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    display: block;
  }

  .cards {
    display: flex;
  }
</style>
