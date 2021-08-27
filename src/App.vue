<template>
  <div id="app">
    <v-app>
      <v-app-bar dark app elevation="0">

      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(100,115,201,.7), rgba(25,32,72,.7)"
        ></v-img>
      </template>
      9/4 怪人報名名單</v-app-bar>
      <v-main class="px-3">
        <div class="d-flex justify-center mt-8" v-if="isLoading">
          <v-progress-circular
            indeterminate
            :size="100"
            color="primary"
          ></v-progress-circular>

        </div>
        <v-card
          class="mx-auto "
          max-width="500"
          tile v-else
        >
          <v-list dense>
              <v-list-item
                v-for="(item, i) in items"
                :key="i"
              >
                <v-list-item-icon>
                  <v-icon v-text="`mdi-account`"></v-icon>
                </v-list-item-icon>
                <v-list-item-content>
                  {{ item[0]? item[0] : '等你報名' }}
                  <!-- <v-list-item-title v-text="item[0]"></v-list-item-title> -->
                </v-list-item-content>
              </v-list-item>
          </v-list>
        </v-card>
        <div class="mt-8 purple--text darken-1 d-flex justify-center">
          一個小要求，如果報名成功後，後來又確定不能來，麻請私訊主辦 (fb:高雄怪奇活動)，可以把名額讓給別人。
        </div>
      </v-main>
    </v-app>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  components: {
  },
  created () {
    this.load()
    // https://script.googleusercontent.com/macros/echo?user_content_key=RQa3UV_bp_A7Ot7b2DI8pf30A6arE2OOTUcokNr27xbC3A-qT0h7SkFfNskX3AbNvZZdqKLHCGlBHlGwxlCpatVoL8S1QuYxm5_BxDlH2jW0nuo2oDemN9CCS2h10ox_1xSncGQajx_ryfhECjZEnCJAaF2O3DjeG585D8Kdya5ggRYxt5IwwZRB3qdeyKo-1Wiw_r0D52gFfrcngihQDv55RuLsdhyDMU741UnYodE3UJ8JiiR8kA&lib=MlIA8paqZQMOFrrZqMEnbFiq1-vRkhSuq
  },
  data: () => ({
    items: [],
    isLoading: false
  }),
  methods: {
    async load () {
      try {
        this.isLoading = true
        const res = await axios.get('https://script.google.com/macros/s/AKfycbwgpc1LqrnlSBjeYHTTfSdzJQ-y-nkZ9oI8Wnr_LXAzrlIwoEzXbEEG-OlK9C2qrYrU/exec')
        this.items = res.data
      } catch (err) {
        console.log('err', err)
      } finally {
        this.isLoading = false
      }
    }
  }
}
</script>

<style lang="scss">

</style>
