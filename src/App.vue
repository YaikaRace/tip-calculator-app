<template>
  <main
    class="flex flex-col items-center min-h-screen min-w-[100vw] md:justify-center"
  >
    <img src="./assets/images/logo.svg" alt="logo" class="p-8 md:mb-14" />
    <div
      class="bg-white w-full p-8 rounded-t-3xl md:grid md:grid-cols-2 md:gap-4 md:max-w-4xl md:rounded-3xl shadow-very-dark-cyan md:shadow-xl"
    >
      <calculatorComp
        @bill="(v) => (bill = Number(v))"
        @tip="(v) => (tip = Number(v))"
        @people="(v) => (people = Number(v))"
        @modified="updateResult()"
        :empty="empty"
      ></calculatorComp>
      <tipResult
        @reset="reset()"
        :tipResult="tipResult"
        :totalResult="totalResult"
        :empty="empty"
      ></tipResult>
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
      empty: true,
    };
  },
  methods: {
    updateResult() {
      if (this.bill && this.tip && this.people) {
        let tip = this.bill * (this.tip / 100);
        this.tipResult = tip / this.people;
        this.totalResult = (this.bill + tip) / this.people;
      } else {
        this.totalResult = 0.0;
        this.tipResult = 0.0;
      }
      if (!this.bill && !this.tip && !this.people) {
        this.empty = true;
      } else {
        this.empty = false;
      }
    },
    reset() {
      this.empty = true;
      this.bill = null;
      this.tip = null;
      this.people = null;
      this.tipResult = 0.0;
      this.totalResult = 0.0;
    },
  },
};
</script>
