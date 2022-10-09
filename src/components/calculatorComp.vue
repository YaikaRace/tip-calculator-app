<template>
  <form class="flex flex-col relative">
    <label for="bill" class="text-grayish-cyan pb-2">Bill</label>
    <input
      type="text"
      placeholder="0"
      id="bill"
      class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right rounded-md"
    />
    <img
      src="../assets/images/icon-dollar.svg"
      alt="dollar icon"
      class="w-3 absolute top-12 left-4"
    />
    <label for="custom" class="text-grayish-cyan pt-8">Select tip %</label>
    <div class="grid grid-cols-2 grid-rows-3 gap-4 mt-4">
      <buttonComp
        @selected="(t) => changeButton(t)"
        v-for="button in buttons"
        :value="button.value"
        ref="buttons"
        :key="button.id"
        >{{ button.value }}%</buttonComp
      >
      <input
        type="text"
        @input="customTip($event.target.value)"
        ref="custom"
        placeholder="Custom"
        id="custom"
        class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right"
      />
    </div>
    <label for="people" class="text-grayish-cyan">Number of People</label>
    <input
      type="text"
      placeholder="0"
      class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right rounded-md"
    />
    <img
      src="../assets/images/icon-person.svg"
      alt="person icon"
      class="w-4 absolute bottom-4 left-4"
    />
  </form>
</template>

<script>
import buttonComp from "./buttonComp.vue";

export default {
  name: "calculatorComp",
  components: {
    buttonComp,
  },
  data() {
    return {
      selectedValue: 0,
      buttons: [
        {
          id: 1,
          value: 5,
        },
        {
          id: 2,
          value: 10,
        },
        {
          id: 3,
          value: 15,
        },
        {
          id: 4,
          value: 25,
        },
        {
          id: 5,
          value: 50,
        },
      ],
    };
  },
  methods: {
    changeButton(target) {
      this.$refs.buttons.forEach((item) => {
        if (item.$el.classList.contains("active")) {
          item.$el.classList.remove("active");
        } else {
          if (item.$el == target) {
            item.$el.classList.add("active");
            this.$refs.custom.value = "";
            this.selectedValue = item.$el.value;
          }
        }
      });
    },
    customTip(newVal) {
      this.$refs.buttons.forEach((item) => item.$el.classList.remove("active"));
      this.selectedValue = newVal;
    },
  },
};
</script>
