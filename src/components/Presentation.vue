<template>
  <section class="presentation">
    <h1>Ce que l'on dit de nous</h1>
    <p>Découvrez les incroyables articles</p>
    <p>et publications qui parlent de Tediber.</p>
  </section>
</template>

<script>
</script>


<style scoped>

  @font-face {
    font-family: 'Canter Bold';
    src: url("../fonts/Canter_Bold.woff2") format('woff2');
  }

  .presentation {
    background-color: #202447;
    color: #fff;
    height: 21rem;
    text-transform: uppercase;
    letter-spacing: 2px;
    margin-top: 4rem;
  }

  h1 {
    font-size: 5rem;
    font-family: 'Canter Bold';
    padding-top: 4rem;
    line-height: 1;
  }

  p {
    font-size: 1.2rem;
    line-height: 1.5rem;
    font-weight: bold;
  }

  .presentation h1::after {
    content: url(../img/zigzag.svg);
    display: block;
    font-size: 1rem;
    margin: 2rem 0;
  }


</style>
