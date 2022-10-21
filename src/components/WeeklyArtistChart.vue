<template>
  <section id="weeklyArtistChart" v-if="Chart">
    <header>
      <h2>Weekly artist chart</h2>
      <p>
        This is your <b>Last.week</b>, the last 7 days of your listening tracks.
        <a :href='weeklyChartURL' target="_blank" rel="noopener noreferrer">See
          more
          <ArrowRight size="14" />
        </a>
      </p>
    </header>
    <div class="grid">
      <a v-for="artist in Chart" :key="artist.name" class="card" :href="artist.url" target="_blank"
         rel="noopener noreferrer">
        <div class="card__content">
          <h3 class="card__title">
            <User size="14" />
            {{ artist.name }}
          </h3>
          <p class="card__artist">
            <Play size="14" />
            {{ artist.playcount }} plays
          </p>
        </div>
      </a>
    </div>
  </section>
</template>

<script>
import { Play, User, ArrowRight } from "lucide-vue-next"

export default {
  name: "WeeklyArtistChart",
  components: {
    ArrowRight,
    Play,
    User
  },
  data() {
    return {
      Chart: Array,
      weeklyChartURL: String
    }
  },
  methods: {
    async getWeeklyArtistChart() {
      const customUsername = localStorage.getItem("customUsername") ? localStorage.getItem("customUsername") : import.meta.env.VITE_USERNAME
      const key = localStorage.getItem("lastfm_key") ? localStorage.getItem("lastfm_key") : import.meta.env.VITE_LASTFM_KEY
      const limit = import.meta.env.VITE_LASTFM_LIMIT_FOR_ARTIST_CHART ? import.meta.env.VITE_LASTFM_LIMIT_FOR_ARTIST_CHART : 10
      const response = await fetch(
        `https://ws.audioscrobbler.com/2.0/?method=user.getweeklyartistchart&user=${customUsername}&api_key=${key}&limit=${limit}&format=json`
      )
      const data = await response.json()
      console.log(data.weeklyartistchart.artist)
      this.Chart = data.weeklyartistchart.artist
      this.weeklyChartURL = `https://www.last.fm/user/${import.meta.env.VITE_USERNAME}/listening-report/week`
    }
  },
  async created() {
    await this.getWeeklyArtistChart()
  }
}
</script>

<style scoped>

</style>