<template>
  <div>
    <div class="lives">
        <img v-if="lives>0" src="@/assets/icons8-pixel-heart-48.png" alt="Lives">
        <img v-else src="@/assets/icons8-pixel-heart-empty.png" alt="Lives">
        <img v-if="lives>1" src="@/assets/icons8-pixel-heart-48.png" alt="Lives">
        <img v-else src="@/assets/icons8-pixel-heart-empty.png" alt="Lives">
        <img v-if="lives>2" src="@/assets/icons8-pixel-heart-48.png" alt="Lives">
        <img v-else src="@/assets/icons8-pixel-heart-empty.png" alt="Lives">
    
        <h2 class="hits"> Hits: {{ hits }}</h2>
    </div>
    
    

  </div>
</template>

<script>

export default {
    props: {
        lives: {
            type: Number,
            required: true
        },
        hits: {
            type: Number,
            required: true
        }
    }
}
</script>

<style scoped>
    .lives {
        z-index: 5;
        position: relative;
    }
</style>

