<template>
  <main class="flex flex-col items-center">
    <img src="./assets/images/logo.svg" alt="logo" class="p-8" />
    <div class="bg-white w-full p-8 rounded-t-3xl">
      <calculatorComp></calculatorComp>
    </div>
  </main>
</template>

<script>
import calculatorComp from "./components/calculatorComp";

export default {
  name: "App",
  components: {
    calculatorComp,
  },
};
</script>
