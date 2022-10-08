<template>
  <button
    type="button"
    @click.prevent="$emit('selected', value)"
    :value="value"
    :class="{ active: active }"
    class="bg-very-dark-cyan text-white py-2 rounded-md hover:bg-strong-cyan hover:text-very-dark-cyan text-2xl"
  >
    <slot>Button</slot>
  </button>
</template>
<script>
export default {
  name: "buttonComp",
  props: {
    value: { default: 0 },
    active: {
      type: Boolean,
      default: false,
    },
  },
};
</script>
