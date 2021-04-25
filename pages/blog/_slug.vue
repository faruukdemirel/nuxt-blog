<template>
  <div >
    <article  class="flex lg:h-screen w-screen lg:overflow-hidden xs:flex-col lg:flex-row">
       <div class="relative lg:w-1/3 xs:w-full xs:h-84 lg:h-full post-left">
       <img :src="article.img" :alt="article.alt"  class="absolute h-full w-full object-cover" />
      <p>Article last updated: {{ formatDate(article.updatedAt) }}</p>
          <div class="flex absolute -mt-6  w-full ">
       <TheHeader class="relative lg:w-full xs:w-full xs:h-84 lg:h-full post-left" />
      </div>
       </div>
      <div
      class="relative xs:py-8 xs:px-8 lg:py-32 lg:px-16 lg:w-1/2 xs:w-full h-full overflow-y-scroll markdown-body post-right custom-scroll"
    >
    <nuxt-content
        class="prose prose-sm sm:prose lg-prose xl:prose-2xl mx-auto"
       :document="article" />
      <author :author="article.author" />
      <prev-next :prev="prev" :next="next" />
      </div>

      
    </article>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content("articles", params.slug).fetch();
    const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch()
    return { 
        article,
        prev,
        next
        };
  },
  methods: {
    formatDate(date) {
      const options = { year: "numeric", month: "long", day: "numeric" };
      return new Date(date).toLocaleDateString("en", options);
    },
  },
};
</script>

<style scoped>
.nuxt-content h2 {
  font-weight: bold;
  font-size: 28px;
}
.nuxt-content h3 {
  font-weight: bold;
  font-size: 22px;
}
.nuxt-content p {
  margin-bottom: 20px;
}
.icon.icon-link {
  background-image: url("~assets/svg/icon-hashtag.svg");
  display: inline-block;
  width: 20px;
  height: 20px;
  background-size: 20px 20px;
}
</style>