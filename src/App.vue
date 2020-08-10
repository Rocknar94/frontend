<script>
import conf from './config.js'
import Vue from 'vue'
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'
import axios from 'axios'

Vue.use(VueMaterial)

export default {
  name: 'App',
  components: {

  },
  data () {
    return {
      posts: []
    }
  },
  mounted () {
    axios
        .get(conf.backend.url + conf.backend.api)
        .then(response => this.posts = response.data.posts)
  }
};
</script>
<template>
  <div id="app">
    <md-table v-model="posts" md-card>
      <md-table-toolbar>
        <h1 class="md-title">Posts</h1>
      </md-table-toolbar>

      <md-table-row slot="md-table-row" slot-scope="item">
        <md-table-cell md-label="ID">{{ item.item.id }}</md-table-cell>
        <md-table-cell md-label="TITLE">{{ item.item.title }}</md-table-cell>
        <md-table-cell md-label="MESSAGE">{{ item.item.body }}</md-table-cell>
        <md-table-cell md-label="AUTHOR ID" md-numeric>{{ item.item.userId }}</md-table-cell>
      </md-table-row>
    </md-table>
  </div>
</template>