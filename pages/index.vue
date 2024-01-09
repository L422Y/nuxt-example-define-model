<template>
  <div>
    <h1>Nuxt/Vue 3 defineModel Examples</h1>
    <p>This is a set of demos for using Vue's defineModel with Nuxt</p>
    <div class="examples">
      <fieldset>
        <legend>
          <button @click="navigateTo('/basic')">Basic Example</button>
        </legend>
        <p>
          Basic implementation of globally shared 2-way binding using
          defineModel and useState
        </p>
      </fieldset>
      <fieldset>
        <legend>
          <button @click="navigateTo('/advanced')">Advanced Example</button>
        </legend>
        <p>
          Implements and accepts two modifiers, "split" and "capitalize" which
          modify the appearance of a property of the in the modal value in a
          non-mutative manner
        </p>
      </fieldset>
    </div>
  </div>
</template>
<script lang="ts" setup></script>
<style>
.examples {
  display: grid;
  gap: 2rem;
}
</style>
