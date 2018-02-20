<template>
  <div class="content">
    <ul>
      <!-- For do vue para a propriedade passada -->
      <li v-for="cards in deck" :key="cards._id" :class="cards.rarity">
        <img :src="'http://www.clashapi.xyz/images/cards/' + cards.idName + '.png'" :alt="cards.name" :title="cards.name">
        <div class="overlay">
          <h2>{{cards.name}}</h2>
          <p>
            {{cards.description}}
          </p>
        </div>
      </li>
    </ul>
    <div class="footer">
      <button v-on:click="getDeck" class="action-button shadow animate red">Gerar deck novo</button>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      deck: [],
      decks: []
    }
  },
  created () {
    // Executa a ação
    this.getDeck()
  },
  methods: {
    getDeck: function () {
      this.$http.get('http://www.clashapi.xyz/api/random-deck').then(function ({data}) {
        this.deck = data
        console.log(this.deck)
      }, (error) => {
        console.log(error)
      })
    }
  }
}
</script>
<style>
@import '../src/assets/css/style.css';
</style>
