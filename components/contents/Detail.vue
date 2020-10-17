<template>
  <div>
    <v-container
      v-for="(content, index) in contents"
      :key="index"
    >
      <h1>
        <name :message="content.title" />
      </h1>
      <nuxt-content :document="content" />
      <v-btn
        class="float-right"
        to="/articles"
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
    }
  },
  data () {
    return {
      contents: []
    }
  },
  mounted () {
    this.getContent()
  },
  methods: {
    async getContent () {
      this.contents = await this.$content(this.contentType).where({ id: this.$route.params.id }).fetch()
    }
  }
}
</script>
