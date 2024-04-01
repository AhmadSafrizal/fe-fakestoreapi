<template>
  <div class="product" v-if="current" :class="bgClass(current.category)">
    <div class="product-card">
      <div class="product-image">
        <img :src="current.image" :alt="current.title" />
      </div>
      <div class="product-info">
        <h3 class="product-name" :class="titleClass(current.category)">{{ current.title }}</h3>
        <div class="product-rate-category">
          <div class="product-category">{{ current.category }}</div>
          <div class="product-rating">
            <span
              v-for="star in 5"
              :key="star"
              class="card__star"
              :class="starClass(star, current.category, current.rating.rate)"
            ></span>
          </div>
        </div>
        <hr />
        <div class="product-details">
          <p>{{ current.description }}</p>
        </div>
        <hr />
        <div class="product-price" :class="priceClass(current.category)">${{ current.price }}</div>
        <div class="product-btn">
          <button class="product-button" :class="buyClass(current.category)">Buy now</button>
          <button
            class="next-product-button"
            :class="nextClass(current.category)"
            @click="nextProduct"
          >
            Next Product
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Product',
  props: {
    products: {
      type: Array,
      required: true
    },
    current: {
      type: Object,
      required: true
    },
    next: {
      type: Function,
      required: true
    }
  },
  methods: {
    nextProduct() {
      this.next()
    },
    bgClass(category) {
      if (category === "men's clothing") {
        return 'bg-man'
      } else if (category === "women's clothing") {
        return 'bg-woman'
      } else {
        return ''
      }
    },
    titleClass(category) {
      if (category === "men's clothing") {
        return 'man-title'
      } else if (category === "women's clothing") {
        return 'woman-title'
      } else {
        return ''
      }
    },
    starClass(star, category, rating) {
      let fullStar = null
      const decimal = String(rating).split('.')[1]

      if (decimal >= 5) {
        fullStar = Math.ceil(rating)
      } else {
        fullStar = Math.floor(rating)
      }

      if (category === "men's clothing") {
        return star <= fullStar ? 'man_filled' : 'man-star'
      } else if (category === "women's clothing") {
        return star <= fullStar ? 'woman_filled ' : 'woman-star'
      } else {
        return ''
      }
    },

    priceClass(category) {
      if (category === "men's clothing") {
        return 'man-price'
      } else if (category === "women's clothing") {
        return 'woman-price'
      } else {
        return ''
      }
    },
    buyClass(category) {
      if (category === "men's clothing") {
        return 'man-btn'
      } else if (category === "women's clothing") {
        return 'woman-btn'
      } else {
        return ''
      }
    },
    nextClass(category) {
      if (category === "men's clothing") {
        return 'man-button-next'
      } else if (category === "women's clothing") {
        return 'woman-button-next'
      } else {
        return ''
      }
    }
  }
}
</script>

<style scoped></style>
