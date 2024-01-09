<template>
  <div>
    <h1>Nuxt defineModel Basic Example</h1>
    <p>This is a demo of using defineModel in a custom, resuable component</p>
    <p>
      The `FilterInput` component can be reused throughout the application, to
      share a value across inputs, we utilize `useState`, but this is extra
      functionality and a `ref` works just as well for independent input values
    </p>
  </div>
  <FilterInput v-model="query" />
  <div class="items">
    <div v-for="item in filteredItems">
      {{ item.name }}
    </div>
  </div>
</template>
<script lang="ts" setup>
const query = useState('query', () => '');
const { data } = useFetch('https://pokeapi.co/api/v2/pokemon?limit=30');

const filteredItems = computed(() =>
  query.value?.length > 0
    ? data?.value?.results.filter((item) => item.name.includes(query.value))
    : data.value?.results
);
</script>
<style>
.items {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
}
</style>
