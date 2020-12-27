<template>
  <div id="app">
    <Header/>
    <Presentation/>
    <!-- serving the Content component for every single press category -->
    <Content category="Presse écrite" v-bind:categoryType='["Journal", "Magazine"]' linkName="lire la suite"/>
    <Content category="Contenu web" v-bind:categoryType='["Site internet", "Blog"]' linkName="découvrir"/>
    <Content category="Télévision" v-bind:categoryType='["Télévision", "M6", "Canal +", "France 2", "BFM"]' linkName="visionner"/>
    <Content category="Radio" v-bind:categoryType='["Radio"]' linkName="écouter"/>
    <!-- <Contentbis/> -->
    <Footer/>
  </div>
</template>

<script>

  import Header from './components/Header.vue';
  import Presentation from './components/Presentation.vue';
  import Content from './components/Content.vue';
  // import Contentbis from './components/Contentbis.vue'
  import Footer from './components/Footer.vue';


  export default {
    name: 'app',
    components: {
      Header,
      Presentation,
      Content,
      // Contentbis,
      Footer
    }
  }
</script>

<style>

  @font-face {
    font-family: 'Gill Sans Std Light';
    src: url("./fonts/Gill_Sans_Std_Light.woff2") format('woff2');
  }

  @font-face {
    font-family: 'Gill Sans Std Regular';
    src: url("./fonts/Gill_Sans_Std_Regular.woff2") format('woff2');
  }

  @font-face {
    font-family: 'Canter Bold';
    src: url("./fonts/Canter_Bold.woff2") format('woff2');
  }

  body, a, p, h1, h2, h3 {
    margin: 0;
  }

  #app {
    font-family: 'Gill Sans Std Light', 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    line-height: 1.5;
    color: #202447;
    /* margin-top: 60px; */
  }

  button {
    border: 0;
    margin: 0;
    padding: 0;
    font-size: 100%;
  }

  button:focus {
    outline:0;
  }

</style>
