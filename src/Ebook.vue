<template>
  <div class="ebook">
    <div class="title-wrapper">
      <div class="left">
        <span class="icon-back icon"></span>
      </div>
      <div class="right">
        <div class="icon-wrapper">
          <span class="icon-cart icon"></span>
        </div>
        <div class="icon-wrapper">
          <span class="icon-person icon"></span>
        </div>
        <div class="icon-wrapper">
          <span class="icon-more icon"></span>
        </div>
      </div>
    </div>
    <div class="read-wrapper">
      <div id="reader"></div>
      <div class="mask">
        <div class="left" @click="prevPage()"></div>
        <div class="center"></div>
        <div class="right" @click="nextPage()"></div>
      </div>
    </div>
    <div class="menu-wrapper">
      <div class="icon-wraper">
        <span class="icon-menu icon"></span>
      </div>
      <div class="icon-wraper">
        <span class="icon-progress icon"></span>
      </div>
      <div class="icon-wraper">
        <span class="icon-bright icon"></span>
      </div>
      <div class="icon-wraper">
        <span class="icon-a icon">A</span>
      </div>
    </div>
  </div>
</template>

<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'
export default {
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
.ebook {
  position: relative;
  .title-wrapper {
    background: white;
    position: absolute;
    top:0;
    left: 0;
    width: 100%;
    height: px2rem(48);
    z-index: 101;
    display: flex;
    box-shadow: 0 px2rem(8) px2rem(8) rgba(0, 0, 0, .15);
    .left {
      flex: 0 0 px2rem(60);
      @include center;
    }
    .right {
      flex: 1;
      display: flex;
      justify-content: flex-end;
      .icon-wrapper {
        flex: 0 0 px2rem(40);
        @include center;
      }
    }
  }
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
  .menu-wrapper {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    z-index: 101;
    background: white;
    display: flex;
    height: px2rem(48);
    box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, .15);
    .icon-wraper {
      flex: 1;
      @include center;
    }
    .icon-progress {
      font-size: px2rem(23);
    }
  }
}
</style>
