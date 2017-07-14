<template lang="pug">
  #app
    VMHeader
    section.section
      nav.nav.has-shadow
        .container
          input.input.is-large(type="text" placeholder="Search songs" v-model="searchQuery")
          a.button.is-info.is-large(@click="search") Search
          a.button.is-danger.is-large &times;
      .container
        p
          small {{ searchMessage }}
      .container.results
        .columns
          .column(v-for="t in tracks")
            | {{ t.name }} - {{ t.artists[0].name }}
    VMFooter
</template>

<script>
import trackService from './services/track'
import VMFooter from './components/layout/Footer.vue'
import VMHeader from './components/layout/Header.vue'

export default {
  name: 'app',
  components: { VMFooter, VMHeader },
  data () {
    return {
      searchQuery: '',
      tracks: []
    }
  },
  methods: {
    search () {
      if (!this.searchQuery) return
      trackService.search(this.searchQuery)
        .then(res => {
          this.tracks = res.tracks.items
        })
    }
  },
  computed: {
    searchMessage () {
      return `We found: ${this.tracks.length} songs!`
    }
  }
}
</script>

<style lang="scss">
@import './scss/main.scss';

.results {
  margin-top: 25px;
}
</style>
