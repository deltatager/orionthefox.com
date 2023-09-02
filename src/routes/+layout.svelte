<script>
  import github from '$lib/images/github.svg'
  import './styles.css'
</script>

<div class="app">
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
  img {
    width: 2em;
    height: 2em;
    object-fit: contain;
  }

  a:hover {
    color: var(--color-theme-1);
  }

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

  @media (min-width: 480px) {
    footer {
      padding: 12px 0;
    }
  }
</style>
