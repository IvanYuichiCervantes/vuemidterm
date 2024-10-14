<template>
  <div class="product-form">
    <h2>Add a New Product</h2>
    <form @submit.prevent="submitProduct">
      <div>
        <label for="name">Product Name:</label>
        <input v-model="product.name" id="name" type="text" required />
      </div>
      <div>
        <label for="price">Price:</label>
        <input v-model="product.price" id="price" type="number" required />
      </div>
      <div>
        <label for="description">Description:</label>
        <textarea v-model="product.description" id="description" required></textarea>
      </div>
      <button type="submit">Add Product</button>

    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: {
        name: '',
        price: 0,
        description: ''
      }
    };
  },
  methods: {
    submitProduct() {
      // Emit the product to the parent component
      this.$emit('add-product', { ...this.product });
      // Clear the form after submitting
      this.product = { name: '', price: 0, description: '' };
    }
  }
};
</script>

<style scoped>
.product-form {
  padding: 2rem;
  background-color:gray;
  border:2px solid  black;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin: 2rem auto;
}

h2 {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 1rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

input,
textarea {
  width: 100%;
  padding: 0.5rem;
  margin-bottom: 1rem;
  border: 5px solid #07ffeef1;
  border-radius: 4px;
  font-size: 1rem;
}

input:focus,
textarea:focus {
  border-color: #4800ff;
  outline: none;
}

button {
  padding: 0.7rem 1.2rem;
  background-color: #00eaff;
  color: #000000;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}

button:hover {
  background-color: #0056b3;
}
</style>

