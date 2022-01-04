<template>
  <div class="max-w-screen-2xl mx-auto px-10">
    <h2 class="text-2xl font-semibold font-mono mb-4">
      {{ attributes.title }}
    </h2>
    <div v-html="html" class="markdown"></div>
    <div class="grid grid-cols-2 sm:grid-cols-3 gap-8">
      <article v-for="(product, index) in attributes.products" :key="index">
        <img class="mx-auto" :src="`../${product.image}`" :alt="product.name" />
        <p class="font-mono">{{ product.name }}</p>
        <button
          class="
            buy-button
            snipcart-add-item
            mt-6
            py-2
            px-4
            bg-gradient-to-r
            from-green-400
            to-blue-500
            hover:from-pink-500 hover:to-yellow-500
            text-white
            font-bold
            rounded-full
            shadow-offset
            hover:shadow-lg
            transition
            duration-300
          "
          :data-item-id="product.sku"
          :data-item-name="product.name"
          :data-item-price="product.price"
          :data-item-image="product.image"
        >
          {{ `$${product.price}` }}
        </button>
      </article>
    </div>
  </div>
</template>

<script>
export default {
  layout: 'guide',
  async asyncData({ params, route }) {
    const guideName = params.slug
    const markdownContent = await import(`~/contents/guides/${guideName}.md`)
    return {
      attributes: markdownContent.attributes,
      html: markdownContent.html,
      currentUrl: route.path,
    }
  },
  head() {
    return {
      title: `${this.attributes.title} | Vue PWA Organic Fruit Shop`,
    }
  },
}
</script>