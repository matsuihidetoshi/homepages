<template>
  <div>
    <v-container>
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
import { mapMutations } from 'vuex'
import Name from '~/components/Name.vue'

export default {
  components: {
    Name
  },
  data () {
    return {
      content: this.$store.state.content
    }
  },
  methods: {
    ...mapMutations({
      set: 'content/set',
      remove: 'content/remove'
    })
  }
}
</script>
