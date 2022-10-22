<template>
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
      <input type="text" autocomplete="false" v-model="customUsername" placeholder="Your username without @">
      <button @click="saveCustomUser" class="save">Save</button>
      <button @click="deleteCustomUser" class="delete">Delete</button>
    </form>
  </div>
</template>

<script>
import { ArrowRight } from "lucide-vue-next"

export default {
  name: "FormKey",
  data() {
    return {
      customUsername: "",
      key: ""
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
  background-color: #dbdbdb;
  border-radius: 5px;

  > p {
    margin-bottom: 1rem;
  }
}

.save {
  background-color: #2b681c;
}

.delete {
  background-color: #c9342a;
}
</style>