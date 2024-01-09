<template>
  <div>
    <div style="margin: 2rem 0">
      {{ item.fullname }}
    </div>
  </div>
</template>
<script lang="ts" setup>
export interface ItemAnnotation {
  fullname: string;
  split: boolean;
}
const [item, modifiers] = defineModel<ItemAnnotation, 'slug' | 'capitalize'>({
  get(value) {
    let modifiedValue = { ...value };
    if (modifiers.capitalize)
      modifiedValue.fullname = modifiedValue.fullname?.toUpperCase();
    if (modifiers.split)
      modifiedValue.fullname = modifiedValue.fullname?.split(' ');
    return modifiedValue;
  },
});
</script>
<style></style>
