<template>
  <main class="main">
    <section class="card">
      <img :src="sadFace" alt="Sad Face" class="card-image" />
      <p class="card-title">This product is unavailable to show</p>
      <button type="button" class="card-btn" @click="nextProduct">Next Product</button>
    </section>
  </main>
</template>

<script>
import sadFace from '../assets/img/sad.png'
export default {
  data() {
    return {
      sadFace
    }
  },
  props: {
    next: {
      type: Function,
      required: true
    }
  },
  methods: {
    nextProduct() {
      this.next()
    }
  }
}
</script>

<style></style>
