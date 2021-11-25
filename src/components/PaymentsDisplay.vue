<template>
  <div class="payments-display-wrapper">
    <div class="item" v-for="(item, idx) in items" :key="idx">
      {{ getFPV }}
    </div>
  </div>
</template>
 
<script>
export default {
  name: "PaymentsDisplay",
  props: {
    items: {
      type: Array,
      default: () => [],
    },
  },
  computed: {
    getFPV() {
      return this.$store.getters.getFullPaymentValue;
    },
  },
};
</script>
 
<style lang="scss" module>