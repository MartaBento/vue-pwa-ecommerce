<template>
  <div class="main">
    <Header />
    <nuxt />
    <Footer />
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
    <script
      id="snipcart"
      src="https://cdn.snipcart.com/themes/v3.3.0/default/snipcart.js"
      data-api-key="OTg0MDc1MGUtYWFlNS00ZGExLTkxZDItYWMxYmJjMTg3MjQwNjM3NzY4NDc1OTQ2NDQ0OTg0" 
    ></script>
  </div>
</template>

<script>
import Header from '~/components/Header.vue'
import Footer from '~/components/Footer.vue'

export default {
  components: {
    Header,
    Footer,
  },
}
</script>