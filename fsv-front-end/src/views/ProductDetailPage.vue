<template>
  <div id="page-wrap" v-if="product">
    <div id="img-wrap">
      <img :src="product.imageUrl" />
    </div>
    <div id="product-details">
      <h1>{{ product.name }}</h1>
      <h3 id="price">${{ product.price }}</h3>
      <p>Average rating: {{ product.averageRating }}</p>
      <button v-if="isAddedToCart" id="already-added" class="add-to-cart">
        {{ product.name }} already added.
      </button>
      <button
        v-else-if="showSuccessMessage"
        id="success-button"
        class="add-to-cart"
      >
        {{ product.name }} added to cart.
      </button>
      <button v-else class="add-to-cart" @click="addToCart">Add to Cart</button>
      <h4>Description</h4>
      <p>{{ product.description }}</p>
    </div>
  </div>
  <NotFoundPage v-else />
</template>

<script>
import axios from "axios";
import NotFoundPage from "./NotFoundPage.vue";
export default {
  name: "ProductDetailPage",
  components: {
    NotFoundPage,
  },
  data() {
    return {
      product: {},
      productId: this.$route.params.id,
      showSuccessMessage: false,
      cartItems: [],
    };
  },
  methods: {
    async addToCart() {
      await axios.post("/api/users/12345/cart", { productId: this.productId });
      this.showSuccessMessage = true;
      setTimeout(() => {
        this.$router.push("/products");
      }, 1500);
    },
  },
  computed: {
    isAddedToCart() {
      return this.cartItems.some((ci) => ci.id === this.productId);
    },
  },
  async created() {
    const { data: productResult } = await axios.get(
      `/api/products/${this.productId}`
    );
    this.product = productResult;
    const { data: cartItemResult } = await axios.get(`/api/users/12345/cart`);
    this.cartItems = cartItemResult;
  },
};
</script>

<style scoped>
#page-wrap {
  margin-top: 16px;
  padding: 16px;
  max-width: 600px;
}

#img-wrap {
  text-align: center;
}

img {
  width: 400px;
}

#product-details {
  padding: 16px;
  position: relative;
}

.add-to-cart {
  width: 100%;
}

#success-button {
  background: green;
}

#already-added {
  background: gray;
}

#price {
  position: absolute;
  top: 24px;
  right: 16px;
}
</style>
