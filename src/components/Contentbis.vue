<template>
  <div>
    <div id="press-cards">
      <div v-for="pressCat in pressSettings" v-bind:key="pressCat.cat">
        <!-- <h1>{{ this.category }}</h1> -->
        <h1>{{ pressCat.cat}}</h1>
        <div class="cards-container">
          <div class="button-container">
            <button class="button before" v-on:click="prevCard(pressCat.id)"/>
          </div>
          <transition-group name="switch" tag="div" class="cards-container">
            <div v-for="card in pressCat.displayedCards" class="card switch-card" v-bind:key="card.title">
              <div class="card-main">
                <div class="ribbon">
                  <div class="card-header">
                    <p class="card-date">{{ newDateFormat(card.date) }}</p>
                    <p class="card-type">{{ card.type }}</p>
                  </div>
                  <img src="../img/triangle.svg" alt="triangle" class="triangle"/>
                </div>
                <img :src="require('../img/'+card.logo+'.jpg')" class="card-logo">
                <p class="card-name">{{ card.name }}</p>
                <p class="card-title">{{ card.title }}</p>
                <p class="card-body">"{{ card.body }}"</p>
              </div>
              <div class="card-bottom">
                <a v-bind:href="card.url" target="_blank" class="card-link">{{ pressCat.linkName }}</a>
              </div>
            </div>
          </transition-group>
          <div class="button-container">
            <button class="button after" v-on:click="nextCard(pressCat.id)"/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  // Press categories and their types:
  // presse écrite : Journal, Magazine
  // contenu web : Site internet, Blog
  // télévision : Télévision, M6, Canal +, France 2, BFM
  // radio : Radio

  /* How this component works:
    The component category and types are passed through the props. Hence we have to call this component for every single category.
    When the component is mounted, all the cards of the press.json file corresponding to this category are pushed into the allCards array.
    Then the first 3 cards of the array are pushed in the displayedCards array. Those are the cards that are displayed.
  */

  const pressSettings = [
    {
      id: 'presse_écrite',
      cat: 'Presse écrite',
      type: ['Journal', 'Magazine'],
      linkName: 'lire la suite',
      allCards: [],
      displayedCards: []
    },
    {
      id: 'contenu_web',
      cat: 'Contenu Web',
      type: ['Site internet', 'Blog'],
      linkName: 'découvrir',
      allCards: [],
      displayedCards: []
    },
    {
      id: 'télévision',
      cat: 'Télévision',
      type: ['Télévision', 'M6', 'Canal +', 'France 2', 'BFM'],
      linkName: 'visionner',
      allCards: [],
      displayedCards: []
    },
    {
      id: 'radio',
      cat: 'Radio',
      type: ['Radio'],
      linkName: 'écouter',
      allCards: [],
      displayedCards: []
    }
  ];




  import press from '../json/press.json';

  export default {
    name: 'press-cards',
    data() {
      return{
        press: press.press,
        pressSettings: pressSettings
      }
    },
    mounted() {

        console.log(this.pressSettings);

        this.pressSettings.forEach( category => {
          this.press.forEach( card => {
            if(category.type.includes(card.type)) {
              category.allCards.push(card);
            }
          });
        });

        // change "i < ?" to change the size of the displayedCards array
        this.pressSettings.forEach( category => {
          for (let i = 0; i < 3; i++) {
            category.displayedCards.push(category.allCards[i]);
          }
        });


    },
    methods: {
      // a method to format the date accordingly to the requirements
      newDateFormat: function(date) {
        const day = date.substring(8, 10);
        const month = date.substring(5, 7);
        const year = date.substring(2, 4);
        const newDate = `${day}.${month}.${year}`;
        return newDate;
      },
      // a method to call the next card to display
      // the first card of the displayedCards array is removed from it
      // the next card is selected from the allCards array and pushed into the displayedCards array
      // if the end of the allCards array is reached, the first card of the allCards array is selected
      nextCard: function(id) {

        for (let i=0; i < this.pressSettings.length; i++) {
          if (this.pressSettings[i].id === id) {

            this.pressSettings[i].displayedCards.shift();
            for (let j = 0; j < this.pressSettings[i].allCards.length; j++) {
              if (this.pressSettings[i].allCards[j].title === this.pressSettings[i].displayedCards[1].title) {
                if (j+1 < this.pressSettings[i].allCards.length) {
                  this.pressSettings[i].displayedCards.push(this.pressSettings[i].allCards[j+1]);
                } else {
                  this.pressSettings[i].displayedCards.push(this.pressSettings[i].allCards[0]);
                }
                break;
              }
            }
          }
        }
      },
      // a method to call the previous card to display
      // the last card of the displayedCards array is removed from it
      // the previous card is selected from the allCards array and unshifted into the displayedCards array
      // if the beginning of the allCards array is reached, the last card of the allCards array is selected
      prevCard: function(id) {

        for (let i=0; i < this.pressSettings.length; i++) {
          if (this.pressSettings[i].id === id) {
            this.pressSettings[i].displayedCards.pop();
            for (let j = 0; j < this.pressSettings[i].allCards.length; j++) {
              if (this.pressSettings[i].allCards[j].title === this.pressSettings[i].displayedCards[0].title) {
                if (j > 0) {
                  this.pressSettings[i].displayedCards.unshift(this.pressSettings[i].allCards[j-1]);
                } else {
                  this.pressSettings[i].displayedCards.unshift(this.pressSettings[i].allCards[this.pressSettings[i].allCards.length-1]);
                }
                break;
              }
            }
          }
        }
      }

    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  @font-face {
    font-family: 'olapic-icons';
    src: url("../fonts/olapic-icons.woff") format('woff');
  }

  h1 {
    font-size: 5rem;
    font-family: 'Canter Bold';
    padding-top: 4rem;
    line-height: 1;
    text-transform: uppercase;
    letter-spacing: 2px;
  }

  h1::after {
    content: url(../img/zigzag.svg);
    display: block;
    font-size: 1rem;
    margin: 2rem 0;
  }

  .cards-container {
    max-width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
  }

  .card {
    display: flex;
    flex-direction: column;
    width: 300px;
    height: 500px;
    margin: 0 1rem;
    border: 0.05rem solid #cbcee8;
    box-shadow: 0 2px 4px 0 rgba(127,124,137,.6);
  }

  .card-main {
    flex-grow: 1;
  }

  .card-header {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin: 1rem 1rem 0 1rem;
    font-size: 1.2rem;
    font-weight: bold;
  }

  .ribbon {
    display: flex;
    flex-direction: column;
  }

  .card-type {
    background-color: #202447;
    color: #fff;
    width: 150px;
    position: relative;
    right: -2rem;
    z-index: 1;
    text-transform: uppercase;
    padding: 0.5rem 0;
  }

  .triangle {
    width: 1rem;
    position: relative;
    right: -1rem;
    align-self: flex-end;
  }

  .card-logo {
    height: 40px;
    margin: 1rem;
  }

  .card-name {
    text-transform: uppercase;
    font-weight: 700;
    font-size: 1.1rem;
    margin: 0 1rem 0.8rem 1rem;
  }

  .card-title {
    font-weight: 700;
    font-size: 1rem;
    margin: 0 1rem;
  }

  .card-body {
    font-size: 1rem;
    flex-grow: 1;
    margin: 1rem;
  }

  .card-bottom {
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 2rem;
  }

  .card-link {
    background-color: #fab200;
    text-decoration: none;
    text-transform: uppercase;
    padding: 0.8rem 2rem;
    color: #fff;
    font-weight: 700;
    font-size: 1.2rem;
    letter-spacing: 1.5px;
  }

  .button-container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-grow: 1;
  }

  .button {
    width: 50px;
    height: 50px;
    text-align: center;
    background-color: #fab200;
    border-radius: 50%;
    color: #fff;
    transition: 0.1s ease;
    font-family: 'olapic-icons';
    font-size: 2em;
  }

  .button:hover, .card-link:hover {
    background-color: rgba(250, 178, 0, 0.69);
  }

  .before::before {
    content: '\e816';
  }

  .after::before {
    content: '\e817';
  }


  /* a transition with the name "switch" is played when the displayed cards change */
  .switch-card {
    transition: all 0.8s;
  }

  .switch-enter, .switch-leave-to {
    opacity: 0;
    transform: translateY(300px);
  }

  .switch-leave-active {
    position: absolute;
    transform: translate(-350px, 300px);
  }




</style>
