<template>
  <div>
    <h1>defineModal: Advanced Example</h1>
    <NuxtLink
      target="_blank"
      to="https://vuejs.org/guide/components/v-model.html#handling-v-model-modifiers"
    >
      Handling v-model modifiers with Vue 3.4
    </NuxtLink>
    and this relevant
    <NuxtLink
      target="_blank"
      to="https://github.com/vuejs/rfcs/discussions/503#discussioncomment-7962227"
    >
      comment from Evan You
    </NuxtLink>
    <h2>v-model.split</h2>
    <ItemAnnotation v-model.split="annotation" />
    <h2>v-model.capitalize</h2>
    <ItemAnnotation v-model.capitalize="annotation" />
    <h2>v-model.split.capitalize</h2>
    <ItemAnnotation v-model.split.capitalize="annotation" />
  </div>
</template>
<script lang="ts" setup>
const annotation = ref({
  fullname: 'test mctesterson',
});
</script>
<style></style>
