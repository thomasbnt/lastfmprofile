<template>
  <div v-if="User">
    <header>
      <div>
        <a :href="User.url" target="_blank" rel="noopener noreferrer" v-if="UserImage">
          <img :src="UserImage" :alt="User.name + '\'s profile'" class="user_image">
        </a>
        <a :href="User.url" target="_blank" rel="noopener noreferrer" v-else>
          <img src="/src/assets/img/no_user.png" :alt="User.name + '\'s profile'" class="user_image">

        </a>
        <div>
          <h1>Hello <a :href="User.url" target="_blank" rel="noopener noreferrer">{{ User.name }}</a></h1>
          <p>{{ UserRegisteredSince }}</p>
          <p><b>{{ User.playcount }} musics played</b>, with <b>{{ User.track_count }} uniques tracks</b> for a total of
            <b>{{ User.album_count }} albums</b> !</p>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: "LFMUser",
  data() {
    return {
      User: "",
      UserImage: "/assets/img/no_user.png",
      UserRegisteredSince: ""
    }
  },
  methods: {
    async getUserInfoFromLastFM() {
      if (localStorage.getItem("lastfm_key")) {
        const customUsername = localStorage.getItem("customUsername") ? localStorage.getItem("customUsername") : import.meta.env.VITE_USERNAME
        const key = localStorage.getItem("lastfm_key") ? localStorage.getItem("lastfm_key") : import.meta.env.LASTFM_KEY
        const response = await fetch(
          `https://ws.audioscrobbler.com/2.0/?method=user.getinfo&user=${customUsername}&api_key=${key}&format=json`
        )
        const data = await response.json()
        console.log(data.user)
        this.User = data.user
        this.UserImage = this.User.image[1]["#text"]
        this.UserRegisteredSince = this.unixTimeToDate(this.User.registered.unixtime)
      }
    },
    unixTimeToDate(unixTime) {
      const date = new Date(unixTime * 1000)
      return `Registered since ${date.toLocaleDateString()}`
    }
  },
  async created() {
    await this.getUserInfoFromLastFM()
  }
}
</script>

<style lang="scss" scoped>

header > div {
  display: flex;
  align-items: center;
  gap: 2rem;
  margin: 2rem 0;
}

.user_image {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  box-shadow: var(--primary) 0 0 0 3px;
  transition: .2s;

  &:hover {
    box-shadow: var(--primary) 0 0 0 6px;
  }
}

@media screen and (max-width: 400px) {
  header > div {
    flex-direction: column;
    align-items: flex-start;
  }
}

</style>
