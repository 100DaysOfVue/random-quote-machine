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

body{
  margin-top: -16px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  height: 100%;
}
</style>
