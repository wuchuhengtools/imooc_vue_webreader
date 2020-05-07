<template>
  <div class="ebook">
    <transition name="slide-down">
      <div class="title-wrapper" v-show="isShowTitle_Menu">
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
    </transition>
    <div class="read-wrapper">
      <div id="reader"></div>
      <div class="mask">
        <div class="left" @click="prevPage()"></div>
        <div class="center" @click="isShowTitle_Menu = !isShowTitle_Menu"></div>
        <div class="right" @click="nextPage()"></div>
      </div>
    </div>
    <transition name="slide-up">
      <div class="menu-wrapper" v-show="isShowTitle_Menu">
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
    </transition>
  </div>
</template>

<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'
export default {
  data() {
    return {
      isShowTitle_Menu: false
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
    &.slide-down-enter, &.slide-down-leave-to {
      transform: translate3d(0, -100%, 0);
    }
    &.slide-down-to, &.slide-down-leave {
      transform: translate3d(0, 0, 0);
    }
    &.slide-down-enter-active, &.slide-down-leave-active {
      transition: all .3s linear;
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
    z-index: 102;
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
    &.slide-up-enter {
      transform: translate3d(0, 100%, 0) ;
    }
    &.slide-up-to {
      transform: translate3d(0, 0, 0);
    }
    &.slide-up-enter-active {
      transition: all .3s linear;
    }
  }
}
</style>
