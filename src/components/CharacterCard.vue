<template>
    <div class="character-card">
      <img :src="character.image" :alt="character.name" />
      <h2>{{ character.name }}</h2>
      <p><strong>Status:</strong> {{ character.status }}</p>
      <p><strong>Species:</strong> {{ character.species }}</p>
      <p><strong>Type:</strong> {{ character.type || 'Unknown' }}</p>
      <p><strong>Gender:</strong> {{ character.gender }}</p>
      <p><strong>Origin:</strong> {{ character.origin.name }}</p>
      <p><strong>Location:</strong> {{ character.location.name }}</p>
    </div>
</template>
  
<script>
  export default {
    name: 'CharacterCard',
    props: {
      character: Object,
    },
  };
</script>
  
<style scoped>
  .character-card {
    border: 1px solid #ccc;
    padding: 16px;
    margin: 16px;
    text-align: center;
  }
  .character-card img {
    width: 150px;
    height: 150px;
    object-fit: cover;
  }
</style>
  