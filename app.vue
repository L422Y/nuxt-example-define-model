<template>
  <main>
    <nav>
      <NuxtLink v-for="route in routes" :to="route.path">
        {{ route.name }}
      </NuxtLink>
    </nav>
    <div>
      <NuxtPage />
    </div>
    <Footer />
  </main>
</template>
<script lang="ts" setup>
const routerOpts = useRouter().options;
const routes = computed(() =>
  routerOpts.routes.map((r) => {
    if (r.name === 'index') r.name = 'home';
    return r;
  })
);
</script>
<style>
nav {
  display: flex;
  gap: 0.5rem;
}
</style>
