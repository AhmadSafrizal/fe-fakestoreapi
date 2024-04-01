<template>
  <main>
    <Product v-if="renderProduct" :next="next" :current="current" />
    <ProductUnavailable v-else="next" :next="next" />
  </main>
</template>

<script>
import ProductUnavailable from '../components/ProductUnavailable.vue'
import Product from '../components/Product.vue'
export default {
  name: 'App',
  components: {
    ProductUnavailable,
    Product
  },
  data() {
    return {
      products: [],
      currentIndex: 0
    }
  },
  computed: {
    current() {
      return this.products[this.currentIndex]
    },
    renderProduct() {
      return (
        this.current &&
        (this.current.category === "men's clothing" || this.current.category === "women's clothing")
      )
    }
  },
  methods: {
    next() {
      if (this.currentIndex < this.products.length - 1) {
        this.currentIndex += 1
      } else {
        this.currentIndex = 0
      }
    }
  },
  mounted() {
    fetch('https://fakestoreapi.com/products')
      .then((response) => response.json())
      .then((data) => {
        const dataProduct = data.filter(
          (product) =>
            product.category === "men's clothing" || product.category === "women's clothing"
        )
        this.products = dataProduct
      })
      .catch((error) => {
        console.error('Terjadi kesalahan dalam mengambil data produk:', error)
      })
  }
}
</script>

<style src="../assets/style/style.css"></style>
<style src="../assets/style/unavailable.css"></style>
/* import '../../assets/style/style.css'; */ /* import '../../assets/style/unavailable.css'; */
