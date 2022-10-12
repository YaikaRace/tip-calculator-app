<template>
  <form class="flex flex-col relative">
    <label for="bill" class="text-grayish-cyan pb-2 flex justify-between"
      >Bill<span ref="billErr" class="text-red hidden"
        >can't be zero</span
      ></label
    >
    <input
      type="text"
      v-model="bill"
      @focusout="checkZero($event.target, this.$refs.billErr)"
      @input="
        checkNumber(bill, $event.target),
          $emit('bill', $event.target.value),
          $emit('modified', $event.target.value)
      "
      placeholder="0"
      ref="bill"
      id="bill"
      class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right rounded-md focus:outline focus:outline-strong-cyan focus:outline-2 focus:border-0"
    />
    <img
      src="../assets/images/icon-dollar.svg"
      alt="dollar icon"
      class="w-3 absolute top-12 left-4"
    />
    <label for="custom" class="text-grayish-cyan pt-8">Select tip %</label>
    <div
      class="grid grid-cols-2 grid-rows-3 gap-4 mt-4 md:grid-cols-3 md:grid-rows-2"
    >
      <buttonComp
        @selected="(t) => changeButton(t)"
        @click="
          $emit('tip', selectedValue),
            $emit('modified', selectedValue),
            checkZero($refs.custom, this.$refs.tipErr)
        "
        v-for="button in buttons"
        :value="button.value"
        ref="buttons"
        :key="button.id"
        >{{ button.value }}%</buttonComp
      >
      <input
        type="tel"
        @focusout="checkZero($event.target, this.$refs.tipErr)"
        @input="
          customTip($event.target.value),
            $emit('modified', $event.target.value),
            $emit('tip', $event.target.value)
        "
        ref="custom"
        placeholder="Custom"
        id="custom"
        class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right rounded-md focus:outline focus:outline-strong-cyan focus:outline-2 focus:border-0"
      />
    </div>
    <span ref="tipErr" class="text-red hidden ml-auto">can't be zero</span>
    <label for="people" class="text-grayish-cyan mt-8 pb-2 flex justify-between"
      >Number of People<span ref="peopleErr" class="text-red hidden"
        >can't be zero</span
      ></label
    >
    <input
      type="tel"
      placeholder="0"
      v-model="people"
      @focusout="checkZero($event.target, this.$refs.peopleErr)"
      @input="
        checkNumber(people, $event.target),
          $emit('people', $event.target.value),
          $emit('modified', $event.target.value)
      "
      ref="people"
      class="bg-very-light-grayish-cyan text-2xl py-2 px-4 text-right rounded-md focus:outline focus:outline-strong-cyan focus:outline-2 focus:border-0"
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
  props: ["empty"],
  data() {
    return {
      bill: null,
      selectedValue: 0,
      people: null,
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
          if (item.$el == target) {
            this.selectedValue = "";
          }
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
      if (isNaN(newVal)) {
        this.$refs.custom.value = "";
        this.selectedValue = "";
        return;
      }
      if (Number(newVal) > 100) {
        newVal = 100;
        this.$refs.custom.value = newVal;
      }
      this.selectedValue = newVal;
    },
    checkNumber(val, target) {
      if (isNaN(val)) {
        let newVal = val.replace(/\D/g, "");
        target.value = newVal;
        switch (val) {
          case this.bill:
            this.bill = newVal;
            break;
          case this.people:
            this.people = newVal;
            break;
          default:
            return;
        }
      }
    },
    checkZero(target, targetErr) {
      if (!target.value) {
        if (target == this.$refs.custom) {
          if (this.selectedValue) {
            targetErr.classList.add("hidden");
            target.classList.remove("border-red", "border-2");
            return;
          }
        }
        targetErr.classList.remove("hidden");
        target.classList.add("border-red", "border-2");
      } else {
        targetErr.classList.add("hidden");
        target.classList.remove("border-red", "border-2");
      }
    },
  },
  updated() {
    if (this.empty) {
      this.bill = null;
      this.people = null;
      this.selectedValue = null;
      this.$refs.custom.value = "";
      this.$refs.buttons.forEach((item) => item.$el.classList.remove("active"));
    }
  },
};
</script>
