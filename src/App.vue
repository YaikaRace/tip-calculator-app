<template>
  <main class="flex flex-col items-center">
    <img src="./assets/images/logo.svg" alt="logo" class="p-8" />
    <div class="bg-white w-full p-8 rounded-t-3xl">
      <calculatorComp
        @bill="(v) => (bill = v)"
        @tip="(v) => (tip = v)"
        @people="(v) => (people = v)"
        @updated="updateResult()"
      ></calculatorComp>
      <tipResult :tipResult="tipResult" :totalResult="totalResult"></tipResult>
    </div>
  </main>
</template>

<script>
import calculatorComp from "./components/calculatorComp";
import tipResult from "./components/tipResultComp.vue";

export default {
  name: "App",
  components: {
    calculatorComp,
    tipResult,
  },
  data() {
    return {
      bill: null,
      tip: null,
      people: null,
      tipResult: 0.0,
      totalResult: 0.0,
    };
  },
  methods: {
    updateResult() {
      if (!this.bill && !this.tip && !this.people) {
        this.tipResult = (this.bill * (this.tip / 100)) / this.people;
        this.totalResult =
          (this.bill + this.bill * (this.tip / 100)) / this.people;
      }
    },
  },
};
</script>
