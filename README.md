# svelte-image-magnifier

> Svelte Image Magnifier

[![NPM](https://img.shields.io/npm/v/svelte-image-magnifier.svg)](https://www.npmjs.com/package/svelte-image-magnifier) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## Install

```bash
npm install --save svelte-image-magnifier
```

## Usage

```svelte
<script>
  import Magnifier from 'svelte-image-magnifier'
  export let name;
</script>

<main>
  <div class="container">
    <section>
      <Magnifier image="/emma.jpeg" largeImage="/emma.jpeg" />
    </section>
    <section>
      <h1>Hello {name}!</h1>
      <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
    </section>
  </div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }
  .container {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
```

## License

MIT © [Tun Lin Phyo](https://github.com/tunlinphyo)
