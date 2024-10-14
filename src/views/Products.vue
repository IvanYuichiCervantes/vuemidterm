<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div>
    <ProductForm @add-product="addProduct" />
    <ProductList :products="products" @edit-product="editProduct" />
    <nav> <router-link to="/home">Home</router-link></nav>
  </div>
</template>

<script>
import ProductForm from '@/components/ProductForm.vue';
import ProductList from '@/components/ProductList.vue';

export default {
  components: {
    ProductForm,
    ProductList
  },
  data() {
    return {
      products: []
    };
  },
  methods: {
    addProduct(product) {
      this.products.push(product);
    },
    editProduct({ index, product }) {
      this.products.splice(index, 1, product);
    }
  }
};
</script>

<style scoped>
nav {
  margin-top: 20px;
}

nav a {
  margin-right: 15px;
  color:black;
  text-decoration: none;
  font-weight: bold;
}
</style>
