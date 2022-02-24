<template>
  <div>
  <nav-bar />
  <carousel />
  <Footer />
  </div>
</template>

<script>
import NavBar from '../components/NavBar.vue'
import Footer from '../components/Footer.vue'
import Carousel from '../components/Carousel.vue'

export default {
  name: 'Home',

  components: {
    NavBar,
    Footer,
    Carousel
  }
}
</script>
