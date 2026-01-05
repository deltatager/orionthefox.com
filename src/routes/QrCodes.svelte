<script>
  import QrCode from '../lib/QrCode.svelte'
</script>

<section>
  <QrCode
    data={'https://t.me/orionthefox'}
    label={'Telegram: @orionthefox'}
    image={'https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Telegram_logo.svg/128px-Telegram_logo.svg.png'}
    dotsOptions={{
      type: 'rounded',
      color: '#289fd9'
    }}
  />
  <QrCode
  data={'https://twitter.com/orionthefox'}
  label={'Twitter: @orionthefox'}
  image={'https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Logo_of_Twitter.svg/292px-Logo_of_Twitter.svg.png'}
  dotsOptions={{
    type: 'rounded',
    color: '#1d9bf0'
  }}
/>
  <QrCode
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
  <QrCode
    data={'https://bsky.app/profile/orionthefox.com'}
    label={'Bluesky: @orionthefox.com'}
    image={'https://upload.wikimedia.org/wikipedia/commons/7/7a/Bluesky_Logo.svg'}
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
  }

  @media (max-width: 960px) {
    section {
      flex-direction: column;
    }
  }
</style>
