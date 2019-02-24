<template>
  <div class="main">
    <h1 v-if="quoteState" class="main__title--up">Random Quote Machine</h1>
    <div class="quote__container">
      <h1 class="main__title--down" v-if="!quoteState">Random Quote Machine</h1>
      <transition mode="out-in" name="slide-fade">
        <h3 v-if="loading" class="quote quote--loading" key="loading">
          <p>Loading...</p>
        </h3>
        <div v-else class="quote" key="info">
          <p> {{ quote  }}</p>
          <p><strong> {{ author }} </strong></p>
        </div>
      </transition>
      <div class="btn__container" :class="[quoteState ? 'btn__container--right' : '']">
        <button :class="[quoteState ? 'btn': 'btn--quote']"
          @click="changeQuoteStauts"
        >
          Get your Quote
        </button>
        <!-- remove the tweet id -->
        <a id="tweet" :href="twitterUrl" class="btn btn__twitter" target="_blank" v-if="quoteState"></a>
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
      loading: false,
      quoteState: false,
      quote: '',
      author: '',
      twitterUrl: ''
    }
  },
  methods: {
    changeQuoteStauts (ev) {
      if (!this.quoteState) {
        this.animateElements(ev.target, ev.target.parentElement)
      }
      this.getQuote()
      // eslint-disable-next-line
      setTimeout(() => {
        this.quoteState = true
        this.loading = false
      }, 2500)
    },
    getQuote () {
      this.loading = true
      axios.get(`https://andruxnet-random-famous-quotes.p.rapidapi.com/?count=1&cat=famous`,
        {
          headers: { 'X-RapidAPI-Key': '25ed2d9f1emshd52da26ac7daa32p1fb264jsn803f1bfb8c17' }
        }
      )
        .then(res => {
          this.quote = res.data[0].quote
          this.author = `— ${res.data[0].author} —`
          this.twitterUrl = `https://twitter.com/intent/tweet?text=${this.quote} ${this.author}`
        })
        .catch(e => console.log(e))
    },
    // remove this function and pass everything to CSS transitions with classes
    animateElements (button, container) {
      this.animateTitle()
      this.animateButton(button)
      this.animateButtonContainer(container)
    },
    animateTitle () {
      const $title = document.getElementsByClassName('main__title--down')
      const moveUp = $title[0].animate([
        { transform: 'translateY(0)' },
        { transform: 'translateY(-252px)' }
      ], {
        duration: 1000,
        fill: 'forwards'
      })
      moveUp.play()
    },
    animateButton (button) {
      // animate button
      const changeSize = button.animate([
        {
          height: '50px',
          width: '181px',
          fontSize: '1.5em'
        },
        {
          height: '40px',
          width: '110px',
          fontSize: '13px'
        }
      ], {
        duration: 500,
        fill: 'forwards'
      })
      changeSize.play()
    },
    animateButtonContainer (container) {
      const moveRight = container.animate([
        { right: '100px' },
        { right: '0' },
        { right: '.4em' }
      ], {
        duration: 1500,
        fill: 'forwards'
      })

      const moveLeft = container.animate([
        { width: '110px' },
        { width: '160px' }
      ],
      {
        duration: 1000,
        delay: 2000,
        easing: 'ease-in-out',
        fill: 'forwards'
      })

      moveRight.play()
      moveLeft.play()
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
  padding: 0;
  animation: scalePadding .5s forwards ease-out;
}

@keyframes scalePadding {
  to {
    padding: 11px 20px;
  }
}

.slide-fade-enter-active, .slide-fade-leave-active{
  transition: all .5s;
}

.slide-fade-leave-to, .slide-fade-enter{
  opacity: 0;
  transform: translateX(100px);
}
</style>
