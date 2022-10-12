<template>
  <button
    type="button"
    @click.prevent="$emit('selected', $event.target)"
    :value="value"
    :class="{ active: active }"
    class="bg-very-dark-cyan text-white py-2 rounded-md hover:bg-light-grayish-cyan hover:text-very-dark-cyan text-2xl focus:outline focus:outline-strong-cyan focus:outline-2"
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
