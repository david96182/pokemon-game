<template>
  <div v-if="!pokemon">
    <div>
        <img src="@/assets/pokeball.gif" alt="Pokeball" />
      </div>
       <h1>Loading...</h1>
    </div>

  <div v-else>
    <pokemonScore
      :lives="lives"
      :hits="hits"/>

    <h1 v-if="!showAnswer">Who's That Pokémon?</h1>
    <h1 v-if="showAnswer && lives <= 0">Game Over</h1>
    <h1 v-if="showAnswer">{{message}}</h1>
  
    <PokemonPicture 
      :pokemonId="pokemon.id" 
      :showPokemon="showPokemon"/>
    <PokemonOptions v-if="!showAnswer"
      :pokemons="pokemonArr"
      @selection="checkAnswer"
    />

    <div v-if="showAnswer && lives > 0" class="fade-in pokemon-container">
      <br> <br>
      <button @click="reset">
        Continue
      </button>
    </div>

    <div v-if="showAnswer && lives <= 0" class="fade-in pokemon-container">
      <br> <br>
      <button @click="newGame">
        New Game
      </button>
    </div>
    

  </div>

</template>

<script>
import PokemonOptions from '../components/PokemonOptions'
import PokemonPicture from '../components/PokemonPicture'
import PokemonScore from '../components/PokemonScore.vue'

import getPokemonOptions from '@/helpers/getPokemonOptions'


export default {
  components: { PokemonPicture, PokemonOptions, PokemonScore },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: '',
      lives: 3,
      hits: 0
    }
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonArr = await getPokemonOptions()

      const rndInt = Math.floor(Math.random() * 4)
      this.pokemon = this.pokemonArr[rndInt]
    },
    checkAnswer(selectedId) {
      this.showPokemon = true
      this.showAnswer = true

      if ( selectedId === this.pokemon.id ){
        this.message = `Correct, ${this.pokemon.name }`
        this.hits = this.hits + 1
      } else {
        this.message = `Oops, was ${ this.pokemon.name }`
        this.lives = this.lives - 1
      }
    },
    newGame() {
      this.pokemonArr = []
      this.mixPokemonArray()
      this.showAnswer = false
      this.showPokemon = false
      this.pokemon = null,
      this.lives = 3,
      this.hits = 0
    },
    reset() {
      this.pokemonArr = []
      this.mixPokemonArray()
      this.showAnswer = false
      this.showPokemon = false
      this.pokemon = null
    }
  },
  mounted() {
    this.mixPokemonArray()
  }

}
</script>

<style scoped>

button {
  font-size: 1.5rem;
  font-weight: var(--normal);
  padding: 1rem;
}
.pokemon-container {
  z-index: 4;
  position: relative;
}
h1 {
  z-index: 5;
  position: relative;
  color: yellow;
  font-size: 40px;
}

</style>