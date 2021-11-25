<template>
  <div id="app">
    <div class="wrapper">
      <header>
        <div class="title">My Personal Costs</div>
      </header>
      <main>
        <PaymentsDisplay :items="paymentsList" />
        <AddPaymentForm @addNewPayment="addNewPayment" />
      </main>
    </div>
  </div>
</template>
 
<script>
import PaymentsDisplay from "./components/PaymentsDisplay";
import AddPaymentForm from "./components/AddPaymentForm";
import { mapMutations } from "vuex";
import { mapGetters } from "vuex";
import { mapActions } from "vuex";

export default {
  name: "App",
  components: {
    AddPaymentForm,
    PaymentsDisplay,
  },
  data() {
    return {
      paymentsList: [],
      selected: "",
    };
  },
  methods: {
    ...mapMutations({
      updatePayments: "setPaymentsListData",
    }),
    ...mapGetters({
      updatePayments: "getPaymentsList",
    }),
    ...mapActions(["loadCategories"]),
    ...mapGetters(["getCategoryList"]),
    fetchData() {
      return [
        {
          date: "28.03.2020",
          category: "Food",
          value: 169,
        },
        {
          date: "24.03.2020",
          category: "Transport",
          value: 360,
        },
        {
          date: "24.03.2020",
          category: "Food",
          value: 532,
        },
      ];
    },
  },
  mounted() {
    if (!this.getCategoryList.length) {
      this.loadCategories();
    }
  },
  addNewPayment(data) {
    this.paymentsList = [...this.paymentsList, data];
  },
  created() {
    this.setPaymentsListData(this.fetchData());
  },
};
</script>
 
<style lang="scss" scoped>
#app {
  text-align: center;
  margin-top: 30px;
}
</style>