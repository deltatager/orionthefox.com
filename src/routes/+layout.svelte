<script>
  import github from '$lib/images/github.svg'
  import Background from './Background.svelte'
  import './styles.css'

  let offsetHeight = 0
</script>

<div class="app" bind:offsetHeight>
  <Background height={offsetHeight} />
  
  <main>
    <slot />
  </main>

  <footer>
    &copy; Orion the Astrology fox, 2023
    <a href="https://github.com/deltatager/orionthefox.com" target="_blank">
      <img src={github} alt="GitHub" />
    </a>
  </footer>
</div>

<style>
  .app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    width: 100%;
    max-width: 64rem;
    margin: 0 auto;
    box-sizing: border-box;
  }

  footer {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 12px;
  }

  footer img {
    width: 2em;
    height: 2em;
    object-fit: contain;
    margin-left: 5px;
  }
</style>
