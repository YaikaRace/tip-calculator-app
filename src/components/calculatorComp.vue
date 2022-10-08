<template>
  <form class="flex flex-col">
    <label for="bill" class="text-grayish-cyan pb-2">Bill</label>
    <input
      type="text"
      placeholder="0"
      id="bill"
      class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right"
    />
    <label for="custom" class="text-grayish-cyan pt-8">Select tip %</label>
    <div class="grid grid-cols-2 grid-rows-3 gap-4 mt-4">
      <buttonComp value="5">5%</buttonComp>
      <buttonComp value="10">10%</buttonComp>
      <buttonComp value="15">15%</buttonComp>
      <buttonComp value="25">25%</buttonComp>
      <buttonComp value="50">50%</buttonComp>
      <input
        type="text"
        placeholder="Custom"
        id="custom"
        class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right"
      />
    </div>
  </form>
</template>

<script>
import buttonComp from "./buttonComp.vue";

export default {
  name: "calculatorComp",
  components: {
    buttonComp,
  },
};
</script>
