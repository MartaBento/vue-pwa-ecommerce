<template>
  <div class="max-w-screen-2xl mx-auto px-10">
    <main>
      <div>
        <section class="mb-10" v-for="(guide, index) in guides" :key="index">
          <div class="post-aside mt-4 mb-4">
            <h3 class="mb-5 underline">
              <nuxt-link :to="guide.attributes.link">{{
                guide.attributes.title
              }}</nuxt-link>
            </h3>
            <p>{{ guide.attributes.description }}</p>
          </div>
          <div
            class="
              grid grid-cols-2
              sm:grid-cols-3
              gap-6
              mb-10
              mx-auto
              justify-center
            "
          >
            <article
              class="justify-center"
              v-for="(product, index) in guide.attributes.products"
              :key="index"
            >
              <img
                class="object-scale-down h-96 w-full"
                :src="product.image"
                :alt="product.name"
              />
              <p class="font-mono flex justify-center">{{ product.name }}</p>
              <div class="flex justify-center gap-6 m-3">
                <button
                  class="
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
                    dark:bg-blue-600
                    dark:hover:bg-blue-700
                    dark:focus:ring-blue-800
                    justify-center
                    place-self-stretch
                  "
                  :data-item-id="product.sku"
                  :data-item-name="product.name"
                  :data-item-price="product.price"
                  :data-item-image="product.image"
                >
                  {{ `€${product.price}` }}
                </button>
              </div>
            </article>
          </div>
        </section>
      </div>
    </main>
  </div>
</template>

<script>
import guides from '~/contents/guides/guides.js'

export default {
  async asyncData({ route }) {
    const promises = guides.map((guide) =>
      import(`~/contents/guides/${guide}.md`)
    )
    return { guides: await Promise.all(promises) }
  },
  head() {
    return {
      title: 'Vue PWA Organic Fruit Shop',
    }
  },
}
</script>