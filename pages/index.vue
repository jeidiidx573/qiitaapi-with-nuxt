<template>
  <v-layout justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-container>
        <v-layout>
          <v-flex xs12 md4>
            <v-text-field
              v-model="search"
              label="Search!!"
            ></v-text-field>
          </v-flex>
          <v-flex xs12 md4>
            <v-btn color="green" @click="getQiita"><v-icon>search</v-icon></v-btn>
          </v-flex>
        </v-layout>
      </v-container>
      <v-card>
        <v-list three-line>
          <template v-for="(q,index) in qiita">
            <v-list-tile>
              <v-list-tile-content>
                {{ q.title }}
              </v-list-tile-content>
            </v-list-tile>
          <hr class="my-3">
          </template>
        </v-list>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'
export default {
  components: {
  },
  created() {
    this.getQiita() // QiitaAPI呼び出し
  },
  data() {
    return {
      qiita: null,
      search: null
    }
  },
  methods: {
    // QiitaAPI呼び出し
    getQiita () {
      axios.get('https://qiita.com/api/v2/items', {
       headers: { "Content-Type": "application/json" },
       params: {
         page: 1,
         per_page: 20,
         query: this.search
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
  }
}
</script>
