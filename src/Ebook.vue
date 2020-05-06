<template>
  <div class="ebook">
    <div class="read-wrapper">
      <div id="reader"></div>
    </div>
  </div>
</template>

<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'
export default {
  methods: {
    showEpub() {
      this.book = new Epub(DOWNLOAD_URL)
      this.rendition = this.book.renderTo('reader', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      this.rendition.display()
    }
  },
  mounted() {
    this.showEpub()
  }
}
</script>

<style lang="scss" scoped>
@import '/assets/styles/global';
</style>
