<template>
  <div class="bg-very-dark-cyan p-8 rounded-2xl mt-8 md:mt-0">
    <div class="flex justify-between mt-4 mb-8 md:mb-16">
      <span class="text-white"
        >Tip Amount<span class="text-grayish-cyan block text-sm"
          >/ person</span
        ></span
      >
      <h1 class="text-strong-cyan text-3xl md:text-5xl">
        ${{ parseFloat(tipAmount).toFixed(2) }}
      </h1>
    </div>
    <div class="flex justify-between mb-8">
      <span class="text-white"
        >Total<span class="text-grayish-cyan block text-sm"
          >/ person</span
        ></span
      >
      <h2 class="text-strong-cyan text-3xl md:text-5xl">
        ${{ parseFloat(totalAmount).toFixed(2) }}
      </h2>
    </div>
    <button
      type="reset"
      :disabled="empty"
      @click="$emit('reset')"
      class="bg-strong-cyan text-very-dark-cyan py-2 rounded-md text-2xl w-full disabled:opacity-30 disabled:bg-light-grayish-cyan disabled:cursor-not-allowed focus:outline focus:outline-white focus:outline-2 hover:bg-light-grayish-cyan md:mt-[16%]"
    >
      RESET
    </button>
  </div>
</template>

<script>
export default {
  name: "tipResult",
  props: ["tipResult", "totalResult", "empty"],
  data() {
    return {
      tipAmount: this.tipResult,
      totalAmount: this.totalResult,
    };
  },
  updated() {
    this.tipAmount = this.tipResult;
    this.totalAmount = this.totalResult;
  },
};
</script>
