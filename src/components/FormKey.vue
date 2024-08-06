<template>
  <details open>
    <summary @click="detailsClick">{{ detailsOpened ? "Hide" : "Show" }} settings</summary>
    <div class="formContent">
      <p>
        If you want test that, you must add your <b>Last.fm key</b>.
        <a href="https://github.com/thomasbnt/lastfmprofile#and-how-to-get-the-lastfm-api-key-" target="_blank" rel="noopener noreferrer"
          >How to get that?
          <ArrowRight size="14" />
        </a>
      </p>
      <form>
        <label for="lastfm_key">Enter your Last.fm key</label>
        <input type="password" autocomplete="false" v-model="key" placeholder="key" id="lastfm_key" />
        <button @click="saveKey" class="save">Save</button>
        <button @click="deleteKey" class="delete">Delete</button>
      </form>
      <form>
        <label for="username">Your Last.fm username</label>
        <input type="text" autocomplete="true" v-model="username" placeholder="username" id="username" />
        <button @click="saveCustomUser" class="save">Save</button>
        <button @click="deleteCustomUser" class="delete">Delete</button>
      </form>
    </div>
  </details>
</template>

<script>
import { ArrowRight } from "lucide-vue-next"

export default {
  name: "FormKey",
  data() {
    return {
      username: localStorage.getItem("username") ? localStorage.getItem("username") : "",
      key: localStorage.getItem("lastfm_key") ? localStorage.getItem("lastfm_key") : "",
      detailsOpened: localStorage.getItem("detailsOpened") ? localStorage.getItem("detailsOpened") : true,
    }
  },
  components: {
    ArrowRight,
  },
  methods: {
    saveCustomUser() {
      if (this.username === "") {
        alert("Please enter your Last.fm username.")
        return
      }
      // Check if username are @
      if (this.username.includes("@")) {
        // Remove @
        this.username = this.username.replace("@", "")
      }
      localStorage.setItem("username", this.username)
      this.$emit("getUserInfoFromLastFM")
      this.$emit("getWeeklyArtistChart")
      this.$emit("getUserRecentTracks")
    },
    deleteCustomUser() {
      if (localStorage.getItem("username")) {
        localStorage.removeItem("username")
      }
    },
    saveKey() {
      if (this.key === "") {
        alert("Please enter your Last.fm key.")
        return
      }
      localStorage.setItem("lastfm_key", this.key)
    },
    deleteKey() {
      if (localStorage.getItem("lastfm_key")) {
        localStorage.removeItem("lastfm_key")
      }
    },
    // Show or hide settings, but not working because open attribute is not reactive
    detailsClick() {
      localStorage.setItem("detailsOpened", this.detailsOpened)
      this.detailsOpened = !this.detailsOpened
    },
  },
  created() {
    // If username is in the URL, save it in localStorage
    if (window.location.href.includes("username=")) {
      const url = new URL(window.location.href)
      const username = url.searchParams.get("username")
      console.info(`Username found in URL: ${username}`)
      localStorage.setItem("username", username)
    }
    // If key is in the URL, save it in localStorage
    if (window.location.href.includes("key=")) {
      const url = new URL(window.location.href)
      const key = url.searchParams.get("key")
      console.info(`Key found in URL: ${key}`)
      localStorage.setItem("lastfm_key", key)
    }
  },
}
</script>

<style lang="scss" scoped>
.formContent {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 1rem;
  background-color: #ffffff;
  border-radius: 5px;

  > p {
    margin-bottom: 1rem;
  }
}

.save {
  border: 1px solid var(--quite-black);
  color: var(--quite-black);
  background-color: white;
}

.delete {
  background-color: #c9342a;
}
</style>
