<template>
  <div class="payment-form-wrapper">
    <input placeholder="Amount" v-model="amount" />
    <input placeholder="Type" v-model="type" />
    <input placeholder="Date" v-model="date" />
    <button>Save!</button>
  </div>
</template>
 
<script>
import { mapMutations } from "vuex";
export default {
  name: "AddPaymentForm",
  data() {
    return {
      amount: "",
      type: "",
      date: "",
    };
  },
  computed: {
    ...mapMutations(["setPaymentsListData"]),

    getCurrentDate() {
      const today = new Date();
      const d = today.getDate();
      const m = today.getMonth() + 1;
      const y = today.getFullYear();
      return `${d}.${m}.${y}`;
    },
  },
  methods: {
    onSaveClick() {
      const data = {
        amount: +this.amount,
        type: this.type,
        date: this.date || this.getCurrentDate,
      };
      this.commit("setPaymentsListData", data);
    },
  },
};
</script>
 
<style lang="scss" module>