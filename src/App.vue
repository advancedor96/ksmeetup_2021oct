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
      10/23 跨域交流名單</v-app-bar>
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
                <v-list-item-avatar>
                  <v-badge
                    :content="i+1"
                    color="green"
                    overlap
                  >
                  <v-icon v-text="`mdi-account`"></v-icon>
                  </v-badge>
                </v-list-item-avatar>

                <v-list-item-content>
                  <strong><h2>{{ item[0] }}</h2></strong>
                  <v-list-item-subtitle>{{ item[1] }}</v-list-item-subtitle>
                  <v-list-item-subtitle>{{ item[2] }}</v-list-item-subtitle>
                  <v-list-item-subtitle>{{ item[3] }}</v-list-item-subtitle>

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
  },
  data: () => ({
    items: [],
    isLoading: false
  }),
  methods: {
    async load () {
      try {
        this.isLoading = true
        const res = await axios.get('https://script.google.com/macros/s/AKfycbwFuT8Bg6q1xrr9Yh-56t50IhD7v5MwpB-xI4m38f3LRKSVcfW8Cl0OBXDy7hZy5bmarg/exec')
        // console.log('res', res.data)

        this.items = []
        res.data.forEach(e => {
          if (e[0] === '') {
            console.log('發現為空，跳過')
            return
          }
          this.items.push(e)
        })
      } catch (err) {
        console.log('err', err)
      } finally {
        // console.log('處理後的: ', this.items)

        this.isLoading = false
      }
    }
  }
}
</script>

<style lang="scss">

</style>
