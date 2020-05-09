<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="menu-wrapper"
           :class="{'hide-box-shadow': isSettingShow || !isTitleMenuShow }"
           v-show="isTitleMenuShow">
        <div class="icon-wraper">
          <span class="icon-menu icon" @click="setSettingShow(0)"></span>
        </div>
        <div class="icon-wraper">
          <span class="icon-progress icon" @click="setSettingShow(1)"></span>
        </div>
        <div class="icon-wraper">
          <span class="icon-bright icon" @click="setSettingShow(2)"></span>
        </div>
        <div class="icon-wraper">
          <span class="icon-a icon" @click="setSettingShow(3)">A</span>
        </div>
      </div>
    </transition>
    <transition name="slide-up">
      <div class="setting-wrap" v-show="isSettingShow">
        <div class="setting-font-size" v-if="tagShow === 3">
          <div class="preview" :style="{'font-size': fontSizeList[0].fontSize + 'px'}">A</div>
          <div class="option">
            <div class="select-wrapper"
                 v-for="(item, index) in fontSizeList"
                 :key="index"
                  @click="setFonSize(item.fontSize)">
              <div class="line"></div>
              <div class="point-wrapper">
                <div class="point" v-show="defaultFontSize === item.fontSize">
                  <div class="small-point">
                  </div>
                </div>
              </div>
              <div class="line"></div>
            </div>
          </div>
          <div class="preview" :style="{'font-size': fontSizeList[fontSizeList.length - 1].fontSize + 'px'}">A</div>
        </div>
        <div class="setting-theme" v-if="tagShow === 2">
          <div class="setting-theme-item"
              v-for="(item, index) in themeList"
              :key="index"
              @click="$emit('setTheme', item.name)">
            <div class="preview"
              :style="{background: item.style.body.background }"
              :class="{'no-border': item.style.body.background !== '#fff'}"></div>
            <div class="text"
            :class="{ 'selected': defaultTheme === item.name }">{{item.name}}</div>
          </div>
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
      tagShow: null
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
    },
    defaultFontSize: {
      type: Number,
      default: 14
    },
    themeList: { type: Array, default: Array },
    defaultTheme: { type: String, default: null }
  },
  methods: {
    setFonSize(fontSize) {
      this.$emit('setFontSize', fontSize)
    },
    setSettingShow(tagShow) {
      if (tagShow === this.tagShow || !this.isSettingShow) {
        this.isSettingShow = !this.isSettingShow
      }
      this.tagShow = tagShow
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
    z-index: 101;
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
            position: relative;
            flex: 0 0 0;
            width: 0;
            height: px2rem(7);
            border-right: px2rem(1) solid #ccc;
            .point {
              position: absolute;
              top: px2rem(-6.5);
              left: px2rem(-10);
              width: px2rem(20);
              height: px2rem(20);
              border-radius: 50%;
              background: white;
              border: px2rem(1) solid #ccc;
              box-shadow: 0 px2rem(4) px2rem(4) rgba(0, 0, 0, .15);
              @include center;
              .small-point {
                width: px2rem(5);
                height: px2rem(5);
                background: #333;
                border-radius: 50%;
              }
            }
          }
        }
      }
    }
    .setting-theme {
      height: 100%;
      display: flex;
      .setting-theme-item {
        flex: 1;
        flex-direction: column;
        display: flex;
        padding: px2rem(5);
        box-sizing: border-box;
        .preview {
          flex: 1;
          border: px2rem(1) solid #ccc;
          box-sizing: border-box;
          &.no-border {
            border: none;
          }
        }
        .text {
          flex: 0 0 px2rem(30);
          font-size: px2rem(16);
          color: #ccc;
          @include center;
          &.selected {
            color: #333;
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
