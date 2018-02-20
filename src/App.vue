<template>
  <div class="content">
    <header>
      Random Deck
    </header>
    <ul>
      <!-- For do vue para a propriedade passada -->
      <li v-for="cards in deck" :key="cards._id" :class="cards.rarity">
        <!-- Passa as váriaveis do for para o card -->
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
      <!-- Botão simples para chamar novamente o metodo de gerar um deck aleatório -->
      <button v-on:click="getDeck" class="action-button shadow animate red">Gerar um deck novo</button>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    // Define as variáveis a serem usadas
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
    // Metodo para gerar o deck
    getDeck: function () {
      // Faz a requisição na URL e gera uma premissa para tratar a resposta
      this.$http.get('http://www.clashapi.xyz/api/random-deck').then(function ({data}) {
        this.deck = data
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
