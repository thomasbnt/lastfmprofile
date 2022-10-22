<template>
  <footer>
    <div class="footer__content">
      <p class="footer__text">
        Made with
        <Music4 size="14" />
        by
        <a href="https://thomasbnt.dev" target="_blank" rel="noopener noreferrer">Thomas Bnt</a>
      </p>
      <p class="footer__text">
        <Zap size="14" />
        Created with Vue.js, Vite, Lucide and Last.fm API. Powered by Netlify.
      </p>
    </div>
    <div class="footer__note">
      <p class="footer__text">
        No affiliation with Last.FM. Last.FM is a registered trademark of Last.FM Ltd.
      </p>
      <p class="footer__text">
        This is an open source project. No data is collected. <a
        href="https://github.com/thomasbnt/lastfmprofile"
        target="_blank"
        rel="noopener noreferrer">
        You can check the code here.
      </a>
      </p>
    </div>
  </footer>
</template>

<script>
import { Music4, Zap } from "lucide-vue-next"

export default {
  name: "mainFooter",
  components: {
    Music4,
    Zap
  }
}
</script>

<style lang="scss" scoped>
.footer {
  &__content {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 1rem 0;
  }

  &__text {
    flex: 1;
  }

  &__note {
    display: flex;
    font-size: 13px;
  }
}

@media screen and (max-width: 900px) {
  .footer__content,
  .footer__note {
    flex-direction: column;
    text-align: center;
  }
}
</style>