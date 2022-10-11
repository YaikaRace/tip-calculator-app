<template>
  <div class="bg-very-dark-cyan p-8 rounded-2xl mt-8">
    <div class="flex justify-between m-t-4 mb-8">
      <span class="text-white"
        >Tip Amount<span class="text-grayish-cyan block text-sm"
          >/ person</span
        ></span
      >
      <h1 class="text-strong-cyan text-3xl">
        ${{ parseFloat(tipAmount).toFixed(2) }}
      </h1>
    </div>
    <div class="flex justify-between mb-8">
      <span class="text-white"
        >Total<span class="text-grayish-cyan block text-sm"
          >/ person</span
        ></span
      >
      <h2 class="text-strong-cyan text-3xl">
        ${{ parseFloat(totalAmount).toFixed(2) }}
      </h2>
    </div>
    <button
      type="reset"
      class="bg-strong-cyan text-very-dark-cyan py-2 rounded-md text-2xl w-full"
    >
      RESET
    </button>
  </div>
</template>

<script>
export default {
  name: "tipResult",
  props: ["tipResult", "totalResult"],
  data() {
    return {
      tipAmount: 0.0,
      totalAmount: 0.0,
    };
  },
};
</script>
