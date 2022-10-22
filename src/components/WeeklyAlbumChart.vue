<template>
  <section id="weeklyAlbumChart" v-if="Chart">
    <header>
      <h2>
        <Library size="24" />
        Weekly album chart
      </h2>
      <p>
        This is your <b>Last.week</b> of albums, the last 7 days of your listening tracks.
        <a :href="weeklyChartURL" target="_blank" rel="noopener noreferrer" v-if="weeklyChartURL">See
          more
          <ArrowRight size="14" />
        </a>
      </p>
    </header>
    <div class="grid" v-if="Chart">
      <a v-for="album in Chart" :key="album.name" class="card" :href="album.url" target="_blank"
         rel="noopener noreferrer">
        <div class="card__content">
          <h3 class="card__title">
            <User size="14" />
            {{ album.name }}
          </h3>
          <div class="card__row">
            <p class="card__rank">
              n°{{ album["@attr"].rank }}
            </p>
            <p class="card__artist">
              <Play size="14" />
              {{ album.playcount }} plays
            </p>
          </div>

        </div>
      </a>
    </div>
    <div class="grid" v-if="Chart.length === 0">
      <div class="card card__nodata">
        <div class="card__content">
          <h3 class="card__title">
            <Frown size="14" />
            No artist found
          </h3>
          <p class="card__artist">
            You didn't listen to any artist in the last 7 days
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { Play, User, ArrowRight, Frown, Library } from "lucide-vue-next"

export default {
  name: "WeeklyAlbumChart",
  components: {
    ArrowRight,
    Play,
    User,
    Frown,
    Library
  },
  data() {
    return {
      Chart: "",
      weeklyChartURL: ""
    }
  },
  methods: {
    async getWeeklyAlbumChart() {
      if (localStorage.getItem("lastfm_key")) {
        const username = localStorage.getItem("username") ? localStorage.getItem("username") : import.meta.env.VITE_USERNAME
        const key = localStorage.getItem("lastfm_key") ? localStorage.getItem("lastfm_key") : import.meta.env.LASTFM_KEY
        const limit = import.meta.env.VITE_LASTFM_LIMIT_FOR_ARTIST_CHART ? import.meta.env.VITE_LASTFM_LIMIT_FOR_ARTIST_CHART : 10
        try {
          const response = await fetch(
            `https://ws.audioscrobbler.com/2.0/?method=user.getWeeklyAlbumChart&user=${username}&api_key=${key}&limit=${limit}&format=json`
          )
          const data = await response.json()
          this.Chart = data.weeklyalbumchart.album
          this.weeklyChartURL = `https://www.last.fm/user/${username}/listening-report/week`
          console.log(this.weeklyChartURL)
        } catch (error) {
          this.weeklyChartURL = ``
        }

      }
    }
  },
  async created() {
    await this.getWeeklyAlbumChart()
  }
}
</script>

<style scoped>
</style>