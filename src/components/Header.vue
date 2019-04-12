<template>
  <transition name="header">
    <div class="header" id="navbar" v-if="showHeader">
      <section class="navbar-left">
        <a href="/" class="logo-container">
          <img src="../img/logo_tediber.svg" alt="Logo Tediber" class="logo"/>
        </a>
        <a href="/">Nos produits</a>
        <a href="/">Le concept</a>
        <a href="/">Avis</a>
      </section>
      <section class="navbar-logo">
        <img src="../img/logo_ours.svg" alt="Logo Ours" class="logo logo-ours"/>
      </section>
      <section class="navbar-right">
        <a href="/">Pub TV</a>
        <a href="/">Blog</a>
        <a href="/">Mon compte</a>
        <p>01 86 95 47 10</p>
        <a href="/" class="logo-container">
          <img src="../img/cart.svg" alt="Cart" class="logo"/>
        </a>
      </section>
    </div>
  </transition>
</template>


<script>
  export default {
    name: 'navbar',
    data() {
      return {
        lastPosition: 0,
        showHeader: true
      }
    },
    methods: {
      // hiding the header on scrolling down
      // showing the header on scrolling up
      handleScroll () {
        // if the current position is above the last position (ie: scrolling down), the header is hidden
        // else (ie: scrolling up), the header is displayed
        if (window.pageYOffset > this.lastPosition) {
          this.showHeader = false;
        } else {
          this.showHeader = true;
        }
        this.lastPosition = window.pageYOffset;
      }
    },
    created () {
      window.addEventListener('scroll', this.handleScroll);
    },
    destroyed () {
      window.removeEventListener('scroll', this.handleScroll);
    }
  }
</script>


<style scoped>

  .header {
    height: 4rem;
    background-color: #fff;
    display: flex;
    justify-content: space-between;
    position: fixed;
    width: 100%;
    top: 0px;
    left: 0px;
    z-index: 2;
    box-shadow: 0 0 .8rem 0 rgba(127,124,137,.65);
    transition: all 0.25s ease-in-out;
  }

  .header-enter, .header-leave-to {
    height: 0;
  }


  .navbar-left, .navbar-logo, .navbar-right {
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .navbar-left, .navbar-right {
    flex: 1;
  }

  .navbar-right {
    justify-content: flex-end;
  }

  .logo {
    height: 3rem;
  }


  /* animation for the bear head */
  @keyframes ours {
    0% { transform: rotate(0); }
    25% { transform: rotate(-20deg); }
    50% { transform: rotate(0deg); }
    75% { transform: rotate(20deg); }
    100% { transform: rotate(0); }
  }

  .logo-ours:hover {
    animation-name: ours;
    animation-duration: 0.5s;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
    animation-play-state: paused;
    animation-fill-mode: none;
    animation-play-state: running;
  }

  a, p {
    text-decoration: none;
    text-transform: uppercase;
    font-weight: 700;
    color: #202447;
    padding: 0.5rem 0.8rem;
  }

  a {
    letter-spacing: 1.5px;
  }

  p {
    margin: 0 0.5rem 0 1.5rem;
  }

  a:hover {
    color: #fab200;
  }
</style>
