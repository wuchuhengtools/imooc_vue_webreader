<template>
  <div class="ebook">
    <title-bar :isTitleMenuShow="isTitleMenuShow"></title-bar>
    <div class="read-wrapper">
      <div id="reader"></div>
      <div class="mask">
        <div class="left" @click="prevPage()"></div>
        <div class="center" @click="isTitleMenuShow = !isTitleMenuShow"></div>
        <div class="right" @click="nextPage()"></div>
      </div>
    </div>
    <menu-bar
      :isTitleMenuShow="isTitleMenuShow"
      :fontSizeList="fontSizeList"
      :defaultFontSize="defaultFontSize"
      @setFontSize="setFontSize"
      ref="menuBar"
      ></menu-bar>
  </div>
</template>

<script>
import Epub from 'epubjs'
import TitleBar from '@/components/TitleBar'
import MenuBar from '@/components/MenuBar'

const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'
export default {
  components: {MenuBar, TitleBar},
  comments: {
    TitleBar,
    MenuBar
  },
  data() {
    return {
      isTitleMenuShow: false,
      fontSizeList: [
        { fontSize: 12 },
        { fontSize: 14 },
        { fontSize: 16 },
        { fontSize: 18 },
        { fontSize: 20 },
        { fontSize: 22 },
        { fontSize: 24 }
      ],
      defaultFontSize: 14
    }
  },
  watch: {
    isTitleMenuShow() {
      this.$refs.menuBar.isSettingShow = false
    }
  },
  methods: {
    prevPage() {
      this.rendition.prev()
    },
    nextPage() {
      this.rendition.next()
    },
    showEpub() {
      this.book = new Epub(DOWNLOAD_URL)
      this.rendition = this.book.renderTo('reader', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      // 渲染电子书
      this.rendition.display()
      // 默认字号
      this.setFontSize(this.defaultFontSize)
    },
    setFontSize(fontSize) {
      if (this.rendition.themes) {
        this.rendition.themes.fontSize(fontSize + 'px')
      }
      this.defaultFontSize = fontSize
    }
  },
  mounted() {
    this.showEpub()
  }
}
</script>
<style lang="scss" scoped>
@import '/assets/styles/global';
.ebook {
  position: relative;
  .read-wrapper {
    .mask {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 100;
      width: 100%;
      height: 100%;
      display: flex;
      .left {
        flex: 0 0 px2rem(100);
      }
      .center {
        flex: 1;
      }
      .right {
        flex: 0 0 px2rem(100);
      }
    }
  }
}
</style>
