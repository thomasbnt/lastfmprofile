<script setup>
import NoteOSS from "./components/noteoss.vue"
import FormKey from "./components/FormKey.vue"
import User from "./components/User.vue"
import RecentTracks from "./components/RecentTracks.vue"
import WeeklyArtistChart from "./components/WeeklyArtistChart.vue"
import WeeklyAlbumChart from "./components/WeeklyAlbumChart.vue"
import MainFooter from "./components/main_footer.vue"
</script>

<template>
  <section>
    <NoteOSS />
    <User />
    <RecentTracks />
    <WeeklyArtistChart />
    <WeeklyAlbumChart />
    <FormKey />
  </section>
  <MainFooter />
</template>
