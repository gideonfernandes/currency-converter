<template>
  <div id="app">
    <h1>Conversor de Moedas</h1>
    <main>
      <Converter currency-one="USD" currency-two="BRL" />
      <Converter currency-one="BRL" currency-two="USD" />
      <Converter currency-one="CAD" currency-two="BRL" />
      <Converter currency-one="BRL" currency-two="CAD" />
      <Converter currency-one="EUR" currency-two="BRL" />
      <Converter currency-one="BRL" currency-two="EUR" />
    </main>
    <Footer />
  </div>
</template>

<script>
  import Converter from './components/Converter';
  import Footer from './components/Footer';

  export default {
    name: 'App',
    components: {
      Converter,
      Footer
    }
  }
</script>

<style>
  body {
    margin: 0;
    padding: 0;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

  #app > h1 {
    margin-top: 45px;
  }

  #app > main {
    margin: 60px auto;
    max-width: 960px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: repeat(1fr, 3);
    grid-gap: 26px;
  }

  @media screen and (max-width: 768px) {
    #app > main {
      grid-template-columns: 1fr;
      grid-template-rows: 1fr;
      grid-gap: 12px;
    }
  };
</style>
