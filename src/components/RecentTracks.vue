<template>
  <section id="recentTracks" v-if="recentTracks">
    <header>
      <h2>
        <Hourglass size="24" />
        Recent tracks
      </h2>
    </header>
    <div class="grid">
      <a
        v-for="track in recentTracks.track.slice(0, this.limit)"
        :key="track.name"
        class="card"
        :href="track.url"
        target="_blank"
        rel="noopener noreferrer"
      >
        <div class="card__image" v-if="track.image[2]['#text']">
          <img :src="track.image[2]['#text']" :alt="track.name" />
        </div>
        <div class="card__content">
          <h3 class="card__title">{{ track.name }}</h3>
          <p class="card__artist" title="Name of the artist or the group">
            <User size="14" />
            {{ track.artist["#text"] }}
          </p>
          <p class="card__album" v-if="track.album['#text']" title="Name of the album">
            <Library size="14" />
            {{ track.album["#text"] }}
          </p>
        </div>
      </a>
    </div>
  </section>
</template>

<script>
import { Library, User, Hourglass } from "lucide-vue-next"

export default {
  name: "RecentTracks",
  components: {
    User,
    Library,
    Hourglass,
  },
  data() {
    return {
      recentTracks: "",
      limit: import.meta.env.VITE_LASTFM_LIMIT_FOR_RECENT_TRACKS ? import.meta.env.VITE_LASTFM_LIMIT_FOR_RECENT_TRACKS : 10,
    }
  },
  methods: {
    async getUserRecentTracks() {
      if (localStorage.getItem("lastfm_key")) {
        const username = localStorage.getItem("username") ? localStorage.getItem("username") : import.meta.env.VITE_USERNAME
        const key = localStorage.getItem("lastfm_key") ? localStorage.getItem("lastfm_key") : import.meta.env.LASTFM_KEY
        const response = await fetch(
          `https://ws.audioscrobbler.com/2.0/?method=user.getrecenttracks&user=${username}&api_key=${key}&limit=${this.limit}&format=json`
        )
        const data = await response.json()
        this.recentTracks = data.recenttracks
      }
    },
  },
  async created() {
    await this.getUserRecentTracks()
  },
}
</script>

<style lang="scss" scoped></style>
