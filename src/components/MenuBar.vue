<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="menu-wrapper"
           :class="{'hide-box-shadow': isSettingShow || !isTitleMenuShow }"
           v-show="isTitleMenuShow">
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
        <div class="setting-font-size">
          <div class="preview" :style="{'font-size': fontSizeList[0].fontSize + 'px'}">A</div>
          <div class="option">
            <div class="select-wrapper"
                 v-for="(item, index) in fontSizeList"
                 :key="index">
              <div class="line"></div>
              <div class="point-wrapper">
                <div class="poin"></div>
              </div>
              <div class="line"></div>
            </div>
          </div>
          <div class="preview" :style="{'font-size': fontSizeList[fontSizeList.length - 1].fontSize + 'px'}">A</div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: 'MenuBar',
  data() {
    return {
      isSettingShow: false,
      test: 24
    }
  },
  props: {
    isTitleMenuShow: {
      type: Boolean,
      default: false
    },
    fontSizeList: {
      type: Array,
      default: Array
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
      display: flex;
      height: 100%;
      .preview {
        flex: 0 0 px2rem(40);
        @include center
      }
      .option {
        display: flex;
        flex: 1;
        .select-wrapper {
          flex: 1;
          display: flex;
          align-items: center;
          &:first-child {
            .line {
              &:first-child {
                border-bottom: none;
              }
            }
          }
          &:last-child {
            .line {
              &:last-child {
                border-bottom: none;
              }
            }
          }
          .line {
            flex: 1;
            height: 0;
            border-bottom: px2rem(1) solid #ccc;
          }
          .point-wrapper {
            flex: 0 0 0;
            width: 0;
            height: px2rem(7);
            border-right: px2rem(1) solid #ccc;
          }
        }
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
    &.hide-box-shadow {
      box-shadow: none;
    }
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
