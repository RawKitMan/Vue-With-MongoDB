<template>
  <div>
    <ProductsListItem v-for="item in productList" :key="item.id" :item="item" />
  </div>
</template>

<script>
import ProductsListItem from "./ProductsListItem.vue";

export default {
  name: "ProductsList",
  components: {
    ProductsListItem,
  },
  props: ["productList"],
};
</script>

<style scoped>
</style>