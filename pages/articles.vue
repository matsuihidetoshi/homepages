<template>
    <v-layout>
    <v-flex class="text-center">
      <h3
        class="mb-5"
      >
        articles
      </h3>
      <v-card
        v-for="(article, index) in articles"
        :key="index"
        class="mb-5"
      >
        <v-card-title>
          <name :message="article.title" />
        </v-card-title>
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>
import Name from '~/components/Name.vue'

export default {
  components: {
    Name
  },
  data () {
    return {
      articles: []
    }
  },
  mounted () {
    this.getArticleList()
  },
  methods: {
    async getArticleList () {
      this.articles = await this.$content('articles').fetch()
    }
  }
}
</script>
<style scoped>

</style>