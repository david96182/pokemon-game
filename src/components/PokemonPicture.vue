<template>
    <div class="pokemon-container">
        <img :src="imgSrc"
        class="hidden-pokemon"
        alt="pokemon">

    <img v-if="showPokemon" 
        :src="imgSrc" 
        class="fade-in"
        alt="pokemon">
    </div>
  
</template>

<script>
export default {
    
    props: {
        pokemonId: {
            type: Number,
            required: true
        },
        showPokemon: {
            type: Boolean,
            required: true,
            default: false
        }
    },
    computed: {
        imgSrc() {
            return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
        }
    }
}
</script>

<style scoped>

.pokemon-container {
    height: 200px;
    position: relative;
}
img {
  height: 200px;
  position: absolute;
  width: 100vw;
  margin-left: -50vw;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;

  z-index: 2;
}
.hidden-pokemon {
    filter: brightness(0);
}
.pokemon-container::before {
  background: url("../assets/circle-spikes.png") no-repeat center center / 100%;
  bottom: -330px;
  content: "";
  height: 800px;
  left: -40px;
  position: absolute;
  width: 500px;
}

</style>