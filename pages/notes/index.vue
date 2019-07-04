<template>
  <v-layout justify-center align-center>
    <v-flex xs12 sm8 md6>
      <Search></Search>
      <v-card>
        <v-list three-line>
          <template v-for="(q,index) in qiita">
            <v-list-tile>
              <v-list-tile-content>
                {{ q.title }}
              </v-list-tile-content>
            </v-list-tile>
          </template>
        </v-list>

        <v-card-text>
          <hr class="my-3">
          <nuxt-link to="/">Home</nuxt-link>
          <br>
          <nuxt-link to="/notes/">Note</nuxt-link>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            flat
            nuxt
            to="/inspire"
          >
            Continue
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'
import Search from '~/components/Search.vue'
export default {
  components: {
    Search // ŒŸõƒtƒH[ƒ€
  },
  created() {
    axios.get('https://qiita.com/api/v2/items', {
     headers: { "Content-Type": "application/json" },
     params: {
       page: 1,
       per_page: 20
     },
     timeout: 15000
    })
    .then(res => {
      this.qiita = res.data
    })
    .catch(err => {
      console.log(err)
    })
  },
  data() {
    return {
      qiita: null
    }
  },
  method() {
    return {
    }
  }
}
</script>
