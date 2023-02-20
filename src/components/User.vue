<template>
  <div v-if="ErrorUserNotFound" class="errNotFound">
    {{ ErrorUserNotFound }}
  </div>
  <section v-if="!User" class="user_not_connected">
    <h1>Hello !</h1>
    <h2>Explore your music habits with personalized Last.fm statistics. Find out more about your listening habits right from this page.</h2>
    <small>To get your profile, insert your Last.fm key in settings section.</small>
  </section>
  <section v-if="User">
    <header>
      <div>
        <a :href="User.url" target="_blank" rel="noopener noreferrer" v-if="UserImage">
          <img :src="UserImage" :alt="User.name + '\'s profile'" class="user_image">
        </a>
        <a :href="User.url" target="_blank" rel="noopener noreferrer" v-else>
          <img src="/img/no_user.png" :alt="User.name + '\'s profile'" class="user_image">

        </a>
        <div>
          <h1>Hello <a :href="User.url" target="_blank" rel="noopener noreferrer">{{ User.name }}</a></h1>
          <p>{{ UserRegisteredSince }}</p>
          <p><b>{{ User.playcount }} musics played</b>, with <b>{{ User.track_count }} uniques tracks</b> for a total of
            <b>{{ User.album_count }} albums</b> !</p>
        </div>
      </div>
    </header>
  </section>
</template>

<script>
export default {
  name: "User",
  data() {
    return {
      User: "",
      UserImage: "/assets/img/no_user.png",
      UserRegisteredSince: "",
      ErrorUserNotFound: ""
    }
  },
  methods: {
    async getUserInfoFromLastFM() {
      if (localStorage.getItem("lastfm_key")) {
        const customUsername = localStorage.getItem("username") ? localStorage.getItem("username") : import.meta.env.VITE_USERNAME
        const key = localStorage.getItem("lastfm_key") ? localStorage.getItem("lastfm_key") : import.meta.env.LASTFM_KEY
        try {
          const response = await fetch(
            `https://ws.audioscrobbler.com/2.0/?method=user.getinfo&user=${customUsername}&api_key=${key}&format=json`
          )
          const data = await response.json()
          this.User = data.user
          this.UserImage = this.User.image[1]["#text"]
          this.UserRegisteredSince = this.unixTimeToDate(this.User.registered.unixtime)
        } catch (error) {
          this.ErrorUserNotFound = `Username not found or no data for ${customUsername}.`
          localStorage.removeItem("username")
        }
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
  justify-content: center;
}

.user_not_connected {
  user-select: none;
  padding: 2rem 30%;
  margin: 8rem auto;
  h2 {
    margin-top: 1rem;
    font-weight: normal;
  }
  @media screen and (max-width: 700px) {
    margin: 3rem auto;
    padding: .4rem 3rem;
  }
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

.errNotFound {
  padding: 0.2rem 1rem;
  background-color: #c9342a;
  color: white;
  text-transform: uppercase;
  border-radius: 5px;
}

</style>
