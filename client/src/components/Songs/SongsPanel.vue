<template>
  <v-layout column>
      <panel title="Songs">
        <v-btn
          slot="action"
          :to="{name: 'songs-create'}"
          class="green"
          light
          medium
          absolute
          right
          middle
          fab>
          <v-icon>add</v-icon>
        </v-btn>
        <div
        v-for="song in songs"
        class="song"
        :key="song.id">
        <v-layout>
          <v-flex xs6>
            <div class="song-title">
              {{song.title}}
            </div>
            <div class="song-artist">
              {{song.artist}}
            </div>
            <div class="song-genre">
              {{song.genre}}
            </div>
            <v-btn
              class="light-green"
              :to="{name: 'song', params: {songId: song.id}}">
              View
            </v-btn>
          </v-flex>
          <v-flex xs6>
            <img class="album-image" :src="song.albumImageUrl" />
          </v-flex>
        </v-layout>
        </div>
      </panel>
  </v-layout>
</template>

<script>
import SongsService from '@/services/SongsService'
export default {
  // components: {
    // Panel // my panel then <my-panel /> instead of <panel />
  // },
  data () {
    return {
      songs: null
    }
  },
  /* async mounted () { // if not async, mount wont work
    // do request to the backend for all the Songs
    this.songs = (await SongsService.index()).data // It will send data in panel
  }, */
  watch: {
    '$route.query.search': {
      immediate: true,
      async handler (value) {
        this.songs = (await SongsService.index(value)).data
      }
    }
  }
}
</script>

<style scoped>
.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}
.album-image {
  width :70%;
  margin:0 auto
}
.song-title {
  font-size: 30px;
}
.song-genre {
  font-size: 24px;
}
.song-artist {
  font-size: 18px;
}
</style>
