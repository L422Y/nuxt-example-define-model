<template>
  <div :class="{ opaque: active || showInput }" class="filter-input">
    <button :class="{ hide: alwaysShow || !showButton }" @click="toggleInput">
      <span>Filter</span>
      <span style="font-size: 1.2em">🔎</span>
    </button>
    <div :class="{ showing: alwaysShow || showInput }" class="input">
      <input
        ref="inputEl"
        v-model="filterValue"
        :placeholder
        @blur="maybeHideInput"
        @focus="active = true"
      />
      <div v-if="!alwaysShow" class="close" @click="hideInput">&times;</div>
    </div>
  </div>
</template>
<script lang="ts" setup>
const passed = withDefaults(
  defineProps<{
    placeholder?: string;
    maxWidth?: string;
    alwaysShow?: boolean;
    save?: boolean;
    opacity?: string;
  }>(),
  {
    placeholder: 'Filter...',
    maxWidth: '100%',
    alwaysShow: false,
    save: true,
    opacity: '1',
  }
);

const { placeholder, maxWidth, alwaysShow, save, opacity } = toRefs(passed);

const filterValue = defineModel<string>();
const showButton = ref(true);
const showInput = ref(false);
const active = ref(false);
const inputEl = ref<HTMLInputElement | null>(null);

const toggleInput = () => {
  showInput.value = true;
  showButton.value = false;
  nextTick(() => {
    inputEl.value?.focus();
  });
};

const hideInput = () => {
  showInput.value = false;
  active.value = false;
  filterValue.value = '';
  setTimeout(() => {
    showButton.value = true;
  }, 400);
};

const maybeHideInput = () => {
  if (
    alwaysShow.value ||
    (filterValue.value != undefined && filterValue.value != '')
  ) {
    return;
  }
  hideInput();
};
</script>
<style lang="scss" scoped>
.filter-input {
  position: relative;
  min-width: 32px;
  transition: all 0.4s;
  text-align: center;
  opacity: v-bind(opacity);

  &:hover {
    opacity: 1;
  }

  &.opaque {
    opacity: 1;
  }

  button {
    position: absolute;
    z-index: 44;
    top: 50%;
    left: 50%;
    width: fit-content;
    height: 32px;
    margin: 0;
    padding: 0;
    cursor: pointer;
    transition: all 0.1s;
    transform: translate(-50%, -50%) scale(1);
    transform-origin: center center;
    opacity: 0.5;
    color: #555;
    border: none;
    background: none;
    display: flex;
    align-items: center;
    background: #ddd;
    border: 1px solid #999;
    padding: 0 2rem;
    box-shadow: inset 0 0 0px #000;
    border-radius: 0.25rem;
    &.hide {
      transform: translate(-50%, -50%) scale(0.3);
      pointer-events: none;
      opacity: 0;
    }

    &:hover {
      box-shadow: inset 0 0 4px #000;

      color: #777;
    }
  }

  .input {
    position: relative;
    display: inline-block;
    overflow: hidden;
    width: 100%;
    max-width: 0;
    padding: 0;
    transition: all 0.4s;

    input {
      position: relative;
      box-sizing: border-box;
      width: 100%;
      padding: 0.5rem;
      transition: all 0.4s;
      color: #888;
      border: 1px solid #222;
      border-radius: 0.25rem;
      background: #ddd;

      &::placeholder {
        color: #444;
      }

      &:focus {
        color: #222;
        border-color: #333;
        outline: none;
      }
    }

    .close {
      position: absolute;
      z-index: 44;
      top: 41%;
      right: 0.5rem;
      display: none;
      width: 18px;
      height: 18px;
      cursor: pointer;
      transition: all 0.4s;
      transform: translate(0, -50%);
      color: #333;
      border: none;
      background: none;
    }

    &.showing {
      max-width: v-bind(maxWidth);
      transition: all 0.4s;

      .close {
        display: block;
      }
    }
  }
}
</style>
