<template>
  <v-layout>
    <v-container>
      <v-row>
        <v-flex
          v-for="(article, index) in articles"
          :key="index"
          v-ripple
          xs12
          sm6
          md4
          class="pa-3"
        >
          <nuxt-link
            :to="'articles/' + article.id"
          >
            <v-card>
              <v-card-title>
                <name :message="article.title" />
              </v-card-title>
              <v-card-text>
                <name :message="article.date" />
              </v-card-text>
            </v-card>
          </nuxt-link>
        </v-flex>
      </v-row>

      <v-pagination
        v-model="page"
        :length="pageLength"
        :total-visible="5"
        @input="getArticleList()"
      />

      <v-btn
        to="/"
        class="
          mt-3
          float-right
        "
      >
        back
      </v-btn>
    </v-container>
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
      articles: [],
      content: null,
      page: 1,
      pageLength: 0,
      limit: 6,
      skip: 0
    }
  },
  mounted () {
    this.getArticleList()
    this.getTotalLength()
  },
  methods: {
    async getArticleList () {
      this.articles = []
      this.skip = (this.page - 1) * this.limit
      this.articles = await this.$content('articles').sortBy('date', 'desc').skip(this.skip).limit(this.limit).fetch()
    },
    async getTotalLength () {
      const articles = await this.$content('articles').fetch()
      this.pageLength = Math.ceil(articles.length / this.limit)
    }
  }
}
</script>
<style scoped>

</style>
