<template>
  <div>
    <h1>
      <name v-if="content" :message="content.title" />
    </h1>
    <name v-if="content" :message="new Date(content.date).toLocaleDateString()" />
    <nuxt-content v-if="content" :document="content" />

    <v-btn
      class="
        mt-3
        mb-3
        float-right
      "
      :href="baseUrl()"
    >
      top
    </v-btn>

    <v-overlay :value="overlay">
      <v-progress-circular
        v-if="!loaded"
        indeterminate
        :size="80"
        :width="10"
      />
    </v-overlay>
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
      content: null,
      overlay: true,
      loaded: false
    }
  },
  mounted () {
    this.getContent().then((contents) => {
      this.content = contents[0]
      this.overlay = false
      this.loaded = true
    })
  },
  methods: {
    async getContent () {
      return await this.$content(this.contentType).where({ id: this.$route.params.id }).fetch()
    },
    baseUrl () {
      return process.env.baseUrl
    }
  }
}
</script>
