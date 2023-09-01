<script>
  import Qr from './Qr.svelte'
</script>

<svelte:head>
  <title>Orion 🌌🦊</title>
  <meta name="description" content="Orion's social media links" />
</svelte:head>

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
  section {
    display: flex;
    justify-content: center;
    align-items: center;
    flex: 0.7;
  }
</style>
