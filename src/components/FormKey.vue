<template>
  <div class="formContent">
    <p>You can, if you want test with your username.</p>
    <form>
      <input type="text" autocomplete="false" v-model="customUsername" placeholder="Your username without @">
      <button @click="saveCustomUser" class="save">Save</button>
      <button @click="deleteCustomUser" class="delete">Delete</button>
    </form>
    <!--    <form>
          <input type="password" autocomplete="false" v-model="key" placeholder="Your Last.fm key here">
          <button @click="saveKey" class="save">Save</button>
          <button @click="deleteKey" class="delete">Delete</button>
        </form>-->
  </div>
</template>

<script>
export default {
  name: "FormKey",
  data() {
    return {
      customUsername: "",
      key: ""
    }
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
@media screen and (max-width: 550px) {
  form {
    display: flex;
    flex-direction: column;
    gap: .4rem;
    width: 100%;
  }
}
.save {
  background-color: #2b681c;
}

.delete {
  background-color: #c9342a;
}
</style>