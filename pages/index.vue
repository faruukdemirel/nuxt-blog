<template> 
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <TheHeader />
        </div>
        <div class="col-md-12">
          <ul>
            <li v-for="article in articles" :key="article.slug" class="m-4">
              <NuxtLink
                :to="{ name: 'blog-slug', params: { slug: article.slug } }"
              >
                <div
                  class="max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl"
                >
                  <div class="md:flex">
                    <div class="md:flex-shrink-0">
                      <img
                        class="h-48 w-full object-cover md:w-48"
                        :src="article.img"
                        :alt="article.title"
                      />
                    </div>
                    <div class="p-8">
                      <div
                        class="uppercase tracking-wide text-sm text-indigo-500 font-semibold"
                      >
                        {{ article.title }}
                      </div>
                      <p>by {{ article.author.name }}</p>
                      <p class="mt-2 text-gray-500">
                        {{ article.description }}
                      </p>
                    </div>
                  </div>
                </div>
              </NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const articles = await $content("articles")
      .only(["title", "description", "img", "slug", "author"])
      .sortBy("createdAt", "asc")
      .fetch();

    return {
      articles,
    };
  },
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
