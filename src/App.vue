<script setup>
import NoteOSS from "./components/noteoss.vue"
import FormKey from "./components/FormKey.vue"
import User from "./components/User.vue"
import RecentTracks from "./components/RecentTracks.vue"
import WeeklyArtistChart from "./components/WeeklyArtistChart.vue"
import MainFooter from "./components/main_footer.vue"
</script>

<template>
  <NoteOSS/>
  <FormKey/>
  <User />
  <RecentTracks />
  <WeeklyArtistChart />

  <mainFooter />
</template>
