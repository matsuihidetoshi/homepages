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
          class="ma-3"
          @click="displayDetail(article)"
        >
          <v-card>
            <v-card-title>
              <name :message="article.title" />
            </v-card-title>
          </v-card>
        </v-flex>
      </v-row>
      <v-btn
        to="/"
        class="float-right"
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
      content: null
    }
  },
  mounted () {
    this.getArticleList()
  },
  methods: {
    async getArticleList () {
      this.articles = await this.$content('articles').fetch()
    },
    displayDetail (article) {
      this.$store.state.content = article
      this.$router.push('/detail')
    }
  }
}
</script>
<style scoped>

</style>
