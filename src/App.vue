<template lang="pug">
  #app
    section.section
      nav.nav.has-shadow
        .container
          input.input.is-large(type="text" placeholder="Search songs" v-model="searchQuery")
          a.button.is-info.is-large(@click="search") Search
          a.button.is-danger.is-large &times;
      .container.results
        p
          small {{ searchMessage }}
        .columns
          .column(v-for="t in tracks") {{ t.name }} - {{ t.artist }}
</template>

<script>
const tracks = [
  { name: 'The Red', artist: 'Chevelle' },
  { name: '21 Questions', artist: '50 Cent' },
  { name: 'Cliffs of Dover', artist: 'Eric Johnson' }
]

export default {
  name: 'app',
  data () {
    return {
      searchQuery: '',
      tracks: []
    }
  },
  methods: {
    search () {
      this.tracks = tracks
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
