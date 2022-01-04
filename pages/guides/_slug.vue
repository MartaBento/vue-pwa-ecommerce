<template>
  <div class="max-w-screen-2xl mx-auto px-10">
    <!-- <h2 class="text-2xl font-semibold font-mono mb-4">
      {{ attributes.title }}
    </h2> -->
    <div v-html="html" class="markdown"></div>
    <div
      class="grid grid-cols-2 sm:grid-cols-3 gap-6 mb-10 mx-auto justify-center"
    >
      <article
        class="justify-center"
        v-for="(product, index) in attributes.products"
        :key="index"
      >
        <img
          class="object-scale-down h-96 w-full"
          :src="`../${product.image}`"
          :alt="product.name"
        />
        <p class="font-mono flex justify-center">{{ product.name }}</p>
        <div class="flex justify-center gap-6 m-3">
          <button
            class="
              buy-button
              snipcart-add-item
              text-white
              bg-blue-700
              hover:bg-blue-800
              focus:ring-4 focus:ring-blue-300
              font-medium
              rounded-full
              text-sm
              px-5
              py-2.5
              text-center
              mb-2
              dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800
              justify-center
              place-self-stretch
            "
            :data-item-id="product.sku"
            :data-item-name="product.name"
            :data-item-price="product.price"
            :data-item-image="product.image"
            :data-item-url="`https://snipcart-nuxtjs-pwa.netlify.com${currentUrl}`"
          >
            {{ `$${product.price}` }}
          </button>
        </div>
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