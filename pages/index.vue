<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-row>
        <v-col cols="12">
          <v-card>
            <v-row>
              <v-col cols="4">
                <v-avatar
                  class="ml-5"
                  size="90"
                >
                  <v-img src="/profile.png" />
                </v-avatar>
              </v-col>
              <v-col cols="8">
                <div
                  class="
                    text-left
                    mt-4
                  "
                >
                  <name
                    message="Matsui"
                    class="
                      d-inline-block
                      font-weight-bold
                      text-h5
                    "
                  />
                  <name
                    message="Hidetoshi"
                    class="
                      d-inline-block
                      font-weight-bold
                      text-h5
                    "
                  />
                  <name message="Web Developer" />
                </div>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>

      <v-card
        v-for="(description, index) in descriptions"
        :key="index"
        class="mb-3"
      >
        <v-img
          v-if="description.image"
          height="200"
          :src="description.image"
        />
        <v-card-title
          class="
            headline
            font-weight-bold
          "
        >
          <name :message="description.title" />
        </v-card-title>
        <v-card-text>
          <p
            v-for="(line, lineIndex) in description.lines"
            :key="lineIndex"
            class="mb-1"
          >
            {{ line }}
          </p>
          <hr class="my-3">
          <v-row>
            <v-spacer />
            <v-btn
              color="primary"
              nuxt
              :to="description.link"
              class="mr-3"
            >
              GO
            </v-btn>
          </v-row>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
import Name from '~/components/Name.vue'
import descriptions from '~/data/descriptions.json'

export default {
  components: {
    Name
  },
  data () {
    return {
      descriptions
    }
  }
}
</script>
