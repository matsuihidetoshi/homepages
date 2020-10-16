<template>
  <div>
    <v-container>
      <h1
        class="
          text-center
          ma-2
        "
      >
        <name :message="title" />
      </h1>

      <v-pagination
        v-model="page"
        :length="pageLength"
        :total-visible="5"
        @input="getContentList()"
      />

      <v-row>
        <v-flex
          v-for="(content, index) in contents"
          :key="index"
          v-ripple
          xs12
          sm6
          md4
          class="pa-3"
        >
          <nuxt-link
            :to="contentType + '/' + content.id"
          >
            <v-card>
              <v-card-title>
                <name :message="content.title" />
              </v-card-title>
              <v-card-text>
                <name :message="content.date" />
              </v-card-text>
            </v-card>
          </nuxt-link>
        </v-flex>
      </v-row>

      <v-pagination
        v-model="page"
        :length="pageLength"
        :total-visible="5"
        @input="getContentList()"
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
  </div>
</template>
<script>
import Name from '~/components/Name.vue'

export default {
  components: {
    Name
  },
  props: {
    contentType: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      contents: [],
      page: 1,
      pageLength: 0,
      limit: 6,
      skip: 0
    }
  },
  mounted () {
    this.getContentList()
    this.getTotalLength()
  },
  methods: {
    async getContentList () {
      this.contents = []
      this.skip = (this.page - 1) * this.limit
      this.contents = await this.$content(this.contentType).sortBy('date', 'desc').skip(this.skip).limit(this.limit).fetch()
    },
    async getTotalLength () {
      const contents = await this.$content(this.contentType).fetch()
      this.pageLength = Math.ceil(contents.length / this.limit)
    }
  }
}
</script>
<style scoped>

</style>
