<template>
  <div class="main">
    <h1 v-if="quoteState" class="main__title--up">Random Quote Machine</h1>
    <div class="quote__container">
      <h1 class="main__title--down" v-if="!quoteState">Random Quote machine</h1>
      <div v-else class="quote">
        <p> {{ quote }} </p>
        <p><strong>- {{ quoteAuthor }} -</strong></p>
      </div>
      <div class="btn__container" :class="[quoteState ? 'btn__container--right' : '']">
        <button :class="[quoteState ? 'btn': 'btn--quote']"
          @click="toogleQuoteStatus"
        >
          Get your Quote
        </button>
        <a :href="twitterUrl" class="btn btn__twitter" target="_blank" v-if="quoteState"></a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'quote',
  data () {
    return {
      quoteState: false,
      quote: '',
      quoteAuthor: '',
      twitterUrl: ''
    }
  },
  methods: {
    toogleQuoteStatus (ev) {
      this.getQuote()
      this.quoteState = true
    },
    getQuote () {
      axios.get(`https://andruxnet-random-famous-quotes.p.rapidapi.com/?count=1&cat=famous`,
        {
          headers: { 'X-RapidAPI-Key': '25ed2d9f1emshd52da26ac7daa32p1fb264jsn803f1bfb8c17' }
        }
      )
        .then(res => {
          this.quote = res.data[0].quote
          this.quoteAuthor = res.data[0].author
          this.twitterUrl = `https://twitter.com/intent/tweet?text=${this.quote} ${this.quoteAuthor}.`
        })
        .catch(e => console.log(e))
    }
  }
}
</script>

<style>
.main {
  min-height: calc(100vh - 82px);
  text-align: center;
  display: grid;
  grid-template-rows: 5em 2fr;
  grid-gap: 5px;
}

.main__title--up{
  grid-row: 1 / 2;
}

.quote__container {
  position: relative;
  padding: .4em;
  grid-row: 2;
  height: 150px;
  width: 50%;
  justify-self: center;
  align-self: center;
  background-color: mistyrose;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.quote{
  width: 90%;
  height: 15vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.quote > p {
  margin: 0;
}

.btn__container{
  position: absolute;
  bottom: .4em;
}

.btn__container--right {
  right: .4em;
}

.btn {
  width: 110px;
  height: 40px;
  vertical-align: middle;
}

.btn--quote {
  width: 181px;
  height: 50px;
  font-size: 1.5em;
}

.btn__twitter{
  width: 40px;
  background: url(../assets/twitter.svg) no-repeat;
  border: none;
  margin-left: 10px;
  padding: 11px 20px;
}
</style>
