<template>
  <div class="quote">
    <h1 v-if="quote" class="quote--up">Random Quote Machine in other div</h1>
    <div class="quote--down">
      <h1 class="quote--down__quote" v-if="quote == false">Random Quote machine</h1>
      <button :class="[quote ? 'btn': 'btn--quote']"
        @click="toogleQuote"
      >
        Get your Quote
      </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'quote',
  data () {
    return {
      quote: false
    }
  },
  methods: {
    toogleQuote () {
      this.quote = !this.quote

      axios.get(`https://andruxnet-random-famous-quotes.p.rapidapi.com/?count=1&cat=famous`,
        {
          headers: { 'X-RapidAPI-Key': '25ed2d9f1emshd52da26ac7daa32p1fb264jsn803f1bfb8c17' }
        }
      )
        .then(res => console.log(res))
        .catch(e => console.log(e))
    },
    getQuote (aasd) {
      console.log(aasd)
    }
  }
}
</script>

<style>
.quote {
  min-height: calc(100vh - 82px);
  text-align: center;
  display: grid;
  grid-template-rows: 5em 2fr;
  grid-gap: 5px;
}

.quote--up{
  grid-row: 1 / 2;
}

.quote--down {
  grid-row: 2;
  height: 300px;
  width: 80%;
  justify-self: center;
  align-self: center;
  background-color: mistyrose;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.btn {
  width: 110px;
  height: 40px;
}

.btn--quote {
  width: 181px;
  height: 50px;
  font-size: 1.5em;
}
</style>
