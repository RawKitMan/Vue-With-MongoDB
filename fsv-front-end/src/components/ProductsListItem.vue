<template>
  <div class="product-container">
    <img class="product-image" :src="item.imageUrl" />
    <div class="details-wrap">
      <h3>{{ item.name }}</h3>
      <p>${{ item.price }}</p>
    </div>
    <button class="remove-button" @click="removeFromCart">
      Remove From Cart
    </button>
  </div>
</template>

<script>
export default {
  name: "ProductsListItem",
  props: ["item"],
  methods: {
    removeFromCart() {
      this.$emit("remove-from-list", this.$props.item.id);
    },
  },
};
</script>
<style scoped>
.product-container {
  align-content: "center";
  border-bottom: 1px solid #ddd;
  display: flex;
  padding: 16px;
  width: 100%;
}

.product-image {
  flex: 1;
  height: 100px;
  max-width: 100px;
}

.details-wrap {
  padding: 0 16px;
  flex: 3;
}

.remove-button {
  flex: 1;
  margin: auto;
}
</style>