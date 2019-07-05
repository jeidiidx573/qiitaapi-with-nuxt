<template>
  <v-layout>
    <v-flex xs12 sm12 >
      <v-card>
        <v-card-actions>
          <v-text-field
            v-model="search"
            label="Search!!"
            class="pr-4"
          ></v-text-field>
          <v-btn color="green" @click="getQiita"><v-icon>search</v-icon></v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
          <hr class="my-3" color="green">
        <v-container fluid>
          <v-layout row wrap align-space-around>
            <v-flex v-for="(q,i) in qiita" :key="q.id" xs4 class="pa-2">
              <v-card  hover :href="q.url" target="_blank" color="grey darken-2" height="180px">
                <v-card-title primary-title>
                  <h4>{{ q.title }}</h4>
                </v-card-title>
                <v-card-text class="grey darken-1">
                  <h5>by {{ q.user.id }}<v-icon small class="pl-3">thumb_up</v-icon> {{ q.likes_count }}</h5>
                  <ul><li v-for="(tag,i_tag) in q.tags">#{{ tag.name }}</li></ul>
                  <p class="pt-2 text-truncate">{{ q.body | truncate(120) }}</p>
                </v-card-text>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from 'axios'
import Vue2Filters from 'vue2-filters'
export default {
  components: {
  },
  mixins: [Vue2Filters.mixin],
  created() {
    this.getQiita() // QiitaAPI呼び出し
  },
  data() {
    return {
      qiita: null,
      search: ''
    }
  },
  methods: {
    // QiitaAPI呼び出し
    getQiita () {
      axios.get('https://qiita.com/api/v2/items', {
       headers: { "Content-Type": "application/json" },
       params: {
         page: 1,
         per_page: 21,
         sort: 'stock',
         query: 'body:' + this.search + '+stocks:>20'
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

<style>
ul {
  padding: 0px;
}
li {
  display: inline;
  padding-right: 4px;
  list-style: none;
}
</style>
