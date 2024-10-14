<template>
  <div>
    <h2>Product List</h2>
    <div class="container">
      <ul v-if="products.length">
        <li v-for="(product, index) in products" :key="index">
          <div v-if="editingIndex === index">
            <input v-model="editingProduct.name" type="text" />
            <input v-model="editingProduct.price" type="number" />
            <textarea v-model="editingProduct.description"></textarea>
            <button @click="saveProduct(index)">Save</button>
          </div>
          <div v-else>
            <strong>{{ product.name }}</strong> - ₱{{ product.price }}
            <p>{{ product.description }}</p>
            <button @click="editProduct(index)">Edit</button>
          </div>
        </li>
      </ul>
      <p v-else>No products available.</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['products'],
  data() {
    return {
      editingIndex: null,
      editingProduct: null,
    };
  },
  methods: {
    editProduct(index) {
      this.editingIndex = index;
      this.editingProduct = { ...this.products[index] };
    },
    saveProduct(index) {
      this.$emit('edit-product', { index, product: this.editingProduct });
      this.editingIndex = null;
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
}

ul {
  list-style: none;
  padding: 0;
  width: 100%;
  max-width: 600px; /* Adjust the max width as needed */
}

li {
  margin-bottom: 1.5rem;
  padding: 1rem;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
  transition: box-shadow 0.2s;
}

li:hover {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

strong {
  font-size: 1.2rem;
  color: #333;
}

p {
  margin: 0.5rem 0;
  color: #666;
}

button {
  padding: 0.5rem 1rem;
  background-color: #007bff;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  margin-top: 0.5rem;
}

button:hover {
  background-color: #0056b3;
}

input,
textarea {
  width: 100%;
  padding: 0.5rem;
  margin-bottom: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
}

input:focus,
textarea:focus {
  border-color: #007bff;
  outline: none;
}
</style>
