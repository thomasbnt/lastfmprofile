<template>

  <details open>
    <summary @click="detailsClick">{{ detailsOpened ? "Hide" : "Show" }} settings</summary>
    <div class="formContent">
      <p>If you want test that, you must add your <b>Last.fm key</b>.
        <a href="https://github.com/thomasbnt/lastfmprofile#and-how-to-get-the-lastfm-api-key-" target="_blank"
           rel="noopener noreferrer">How to get that?
          <ArrowRight size="14" />
        </a>
      </p>
      <form>
        <input type="password" autocomplete="false" v-model="key" placeholder="Your Last.fm key here">
        <button @click="saveKey" class="save">Save</button>
        <button @click="deleteKey" class="delete">Delete</button>
      </form>
      <form>
        <input type="text" autocomplete="false" v-model="customUsername" placeholder="Your Last.FM username">
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
      customUsername: "",
      key: "",
      detailsOpened: localStorage.getItem("detailsOpened") ? localStorage.getItem("detailsOpened") : true
    }
  },
  components: {
    ArrowRight
  },
  methods: {
    saveCustomUser() {
      if (this.customUsername === "") {
        alert("Please enter your Last.fm username.")
        return
      }
      // Check if username are @
      if (this.customUsername.includes("@")) {
        // Remove @
        this.customUsername = this.customUsername.replace("@", "")
      }
      localStorage.setItem("customUsername", this.customUsername)
      this.$emit("getUserInfoFromLastFM")
      this.$emit("getWeeklyArtistChart")
      this.$emit("getUserRecentTracks")
    },
    deleteCustomUser() {
      if (localStorage.getItem("customUsername")) {
        localStorage.removeItem("customUsername")
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
    }
  },
  created() {
    // If username is in the URL, save it in localStorage
    if (window.location.href.includes("username=")) {
      const url = new URL(window.location.href)
      const username = url.searchParams.get("username")
      console.info(`Username found in URL: ${username}`)
      localStorage.setItem("customUsername", username)
    }
    // If key is in the URL, save it in localStorage
    if (window.location.href.includes("key=")) {
      const url = new URL(window.location.href)
      const key = url.searchParams.get("key")
      console.info(`Key found in URL: ${key}`)
      localStorage.setItem("lastfm_key", key)
    }
  }
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
  border: 1px solid #2b681c;
  color: #2b681c;
  background-color: white;
}

.delete {
  background-color: #c9342a;
}
</style>