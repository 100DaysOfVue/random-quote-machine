<template>
  <div id="app">
    <Quote />
    <Footer />
  </div>
</template>

<script>
import Footer from './components/layout/Footer.vue'
import Quote from './components/Quote.vue'

export default {
  name: 'app',
  components: { Footer, Quote }
}
</script>

<style>
html, body{
  margin: 0;
  padding: 0;
  height: 100%;
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: inherit;
}

:root{
  --quote-height: 15vh;
  --quote-container-height: 150px;
  --quote-container-width: 50%;
  --quote-container-background: mistyrose;
  --animation-move-up: 252px;
  --links-color: black;
  --links-color-visited: red;
  --btn-color: gray;
  --btn-background-color: lightblue;
  --footer-height: 82px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  height: 100%;
}

.footer {
  height: var(--footer-height);
  text-align: center;
  padding: 2px
}

.footer p {
  margin: .40em;
}
</style>
