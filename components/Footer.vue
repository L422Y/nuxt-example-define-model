<template>
  <footer>
    <div v-if="query">
      <h3>Didn't find what you were looking for?</h3>
      <p>Try adjusting your search:</p>
      <FilterInput v-model="query" alwaysShow />
    </div>
    <div>&copy; 1990 ACME Props</div>
  </footer>
</template>
<script lang="ts" setup>
const query = useState('query', () => '');
</script>
<style scoped>
footer {
  padding: 2rem;
  background: #eee;
  margin-top: 1rem;
  display: grid;
  gap: 1rem;
}
</style>
