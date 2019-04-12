<template>
  <section class="contact">
    <h1>Contact presse</h1>
    <h2>N'hésitez pas à contacter notre équipe presse :</h2>
    <div class="mail-et-tel">
      <p>Elodie : elodie@pascalevenot.com</p>
      <p>Margot : margot@pascalevenot.com</p>
      <p>ou au 01.53.53.44.54</p>
    </div>
    <div class="commentaire">
      <p>Nous vous partagerons les dernières actualités de Tediber</p>
      <p>et répondrons à vos questions.</p>
    </div>
  </section>
</template>

<script>
</script>


<style scoped>

  .contact {
    height: 21rem;
  }

  h1 {
    font-size: 5rem;
    font-family: 'Canter Bold';
    padding-top: 4rem;
    line-height: 1;
    text-transform: uppercase;
    letter-spacing: 2px;
  }

  h2 {
    font-size: 1.7rem;
    line-height: 1.5rem;
    text-transform: uppercase;
    font-family: 'Gill Sans Std Regular';
    font-weight: 400;
  }

  .contact h1::after {
    content: url(../img/zigzag.svg);
    display: block;
    font-size: 1rem;
    margin: 2rem 0 3rem 0;
  }

  .mail-et-tel {
    margin: 2rem 0;
  }

  .commentaire {
    margin-bottom: 5rem;
  }

  p {
    font-size: 1.3rem;
    font-family: 'Gill Sans Std Light';
  }


</style>
