<template>
  <v-layout>
    <content-list content-type="articles" title="記事一覧" />
  </v-layout>
</template>
<script>
import ContentList from '~/components/contents/List.vue'

export default {
  components: {
    ContentList
  }
}
</script>
