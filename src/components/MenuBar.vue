<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="menu-wrapper" v-show="isTitleMenuShow">
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
          <span class="icon-a icon" @click="isSettingShow = !isSettingShow">A</span>
        </div>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="setting-wrap" v-show="isSettingShow">
        <div class="setting-font-size"></div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'MenuBar',
  data() {
    return {
      isSettingShow: false
    }
  },
  props: {
    isTitleMenuShow: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/styles/global";
.menu-bar {
  .setting-wrap {
    position: absolute;
    bottom: px2rem(48);
    left: 0;
    width: 100%;
    height: px2rem(60);
    background: white;
    box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, .15);
    .setting-font-size {
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
  }
}
</style>
