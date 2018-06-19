<template>
  <div id="app" :style="[style.color, style.background]">
    <div id="left">
      <div class="typing">
        <div class="element"></div>
      </div>
    </div>
    <div id="right" :style="style.borderColor">
      <div class="content">
        <p>We are a multidisciplinary research, design and development studio based in Berlin, DE.</p>
        <p>Contact us at <a href="mailto:info@bin.am" :style="[style.color, style.borderColor]">studio@bin.am</a></p>
      </div>
    </div>
  </div>
</template>

<script>
import Typed from 'typed.js'

export default {
  name: 'app',
  data () {
    return {
      colors: [
        ['rgb(30,30,30)', 'rgb(245,245,245)'],
        ['rgb(220,220,220)', 'rgb(30,30,30)'],
        ['rgb(230,230,230)', 'rgb(255,30,30)'],
        ['rgb(220,220,220)', 'rgb(30,30,255)'],
        ['rgb(255,30,30)', 'rgb(255,255,0)']
      ],
      cursors: [
        '░', '▌', '⌇', '░', '⧮', '⧘', '░', '⋮', '░', '♧', '░'
      ],
      style: {}
    }
  },
  mounted: function () {
    let selectedColors = this.randomChoice(this.colors)

    this.style = {
      color: {
        'color': selectedColors[0]
      },
      background: {
        'background': selectedColors[1]
      },
      borderColor: {
        'border-color': selectedColors[0]
      }
    }

    let typed = new Typed('.element', {
      strings: ["Bin ^300"],
      startDelay: 250,
      cursorChar: this.getCursor,
      typeSpeed: 180,
      onComplete: this.showRight
    })
  },
  computed: {
    getCursor: function () {
      return this.randomChoice(this.cursors)
    }
  },
  methods: {
    showRight () {
      document.body.classList.add('show-right')
    },
    randomChoice (arr) {
      return arr[Math.floor(arr.length * Math.random())];
    }
  }
}
</script>

<style>
body, html {
  font-family: 'IBM Plex Mono', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}

.typed-cursor {
  margin-left: 0.1em;
}

.typed-cursor.typed-cursor--blink {
  animation: typedjsBlink 1s infinite !important;
  animation-duration: 1s !important;
}

a {
  color: rgb(220,220,220);
  text-decoration: none;
  border-bottom: 1px dotted rgb(220,220,220);
}

body.show-right {
  #left {
    width: 50vw;
  }
  #right {
    right: 0;
  }
}

#left, #right {
  transition: all 0.3s ease-out;
}

#left {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  width: 100vw;
  display: flex;
  align-items: center;
  justify-content: center;
}

#right {
  position: fixed;
  top: 0;
  right: calc(-50vw - 3px);
  bottom: 0;
  width: 50vw;
  font-size: 24px;
  border-left: 3px solid rgb(220,220,220);
  display: flex;
  align-items: center;
  justify-content: center;
}

.content {
  padding: 0 6rem;
}

.typing {
  margin-top: -0.1em;
  font-size: 8vw;
  display: flex;
}

/* Smartphones (portrait) ----------- */
@media only screen and (max-width : 640px) {
  #left {
    width: 100vw;
    height: 90vh;
  }
  #right {
    height: 50vh;
    width: 100vw;
    top: 100vh;
    right: 0;
    left: 0;
    border-left: 0;
    border-top: 3px solid white;
    font-size: 16px;
    text-align: center;
  }
  body.show-right {
    #left {
      width: 100vw;
      height: 43vh;
    }
    #right {
      top: 41vh;

      .content {
        padding: 0 3rem;
      }
    }
  }
}
</style>
