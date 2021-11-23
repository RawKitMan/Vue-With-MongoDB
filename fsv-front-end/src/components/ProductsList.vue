<template>
  <div>
    <ProductsListItem
      v-for="item in productList"
      :key="item.id"
      :item="item"
      @remove-from-list="removeFromCart"
    />
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
  methods: {
    removeFromCart(event) {
      this.$emit("remove-from-cart", event);
    },
  },
};
</script>

<style scoped>
</style>