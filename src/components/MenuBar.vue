<template>
  <div class="menu-bar">
    <transition name="slide-up">
      <div class="menu-wrapper"
           :class="{'hide-box-shadow': isSettingShow || !isTitleMenuShow }"
           v-show="isTitleMenuShow">
        <div class="icon-wraper">
          <span class="icon-menu icon" @click="setSettingShow(4)"></span>
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
        <div class="setting-font-size" v-if="tabShow === 3">
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
        <div class="setting-theme" v-if="tabShow === 2">
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
        <div class="setting-progress" v-if="tabShow === 1">
          <div class="progress-wrapper">
            <input class="progress" type="range"
            max="100"
            min="0"
            step="1"
            @change="$emit('pageRedirect', $event.target.value)"
            @input="onProgressInput($event.target.value)"
            :value="progress"
            :disabled="!isBookProgressAvalable"
            ref="progress">
          </div>
          <div class="text-wrapper">
            <span>{{isBookProgressAvalable ? progress + '%' : '加载中...'}}</span>
          </div>
        </div>
      </div>
    </transition>
    <directory
      v-show="tabShow === 4"
      :navication="navication"
      :isBookProgressAvalable="isBookProgressAvalable"
      @toPage="toPage"></directory>
    <transition name="fade">
      <div class="content-mask"
      v-show="tabShow === 4"
      @click="tabShow = null">
      </div>
    </transition>

  </div>
</template>

<script>
import Directory from './Directory'
export default {
  name: 'MenuBar',
  components: {Directory},
  comments: {
    Directory
  },
  data() {
    return {
      isSettingShow: false,
      tabShow: 0
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
    defaultTheme: { type: String, default: null },
    isBookProgressAvalable: { type: Boolean, default: false },
    progress: { type: Number, default: 0 },
    navication: Object
  },
  methods: {
    onProgressInput(progress) {
      this.$emit('setProgress', parseInt(progress))
      this.$refs.progress.style.backgroundSize = `${progress}% 100%`
    },
    setFonSize(fontSize) {
      this.$emit('setFontSize', fontSize)
    },
    setSettingShow(tabShow) {
      if (tabShow === this.tabShow || !this.isSettingShow) {
        this.isSettingShow = !this.isSettingShow
      }
      if (tabShow === 4) {
        this.isSettingShow = 0
        this.tabShow = this.tabShow === 4 ? null : tabShow
      } else {
        this.tabShow = tabShow
      }
    },
    toPage(href) {
      this.$emit('toPage', href)
      this.tabShow = null
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
    .setting-progress {
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
      width: 100%;
      height: 100%;
      .progress-wrapper {
        width: 100%;
        height: 100%;
        @include center;
        padding: 0 px2rem(30);
        box-sizing: border-box;
        .progress {
          width: 100%;
          -webkit-appearance: none;
          height: px2rem(2);
          background: -webkit-linear-gradient(#999, #999) no-repeat, #ddd;
          background-size: 0 100%;
          &:focus {
            outline: none;
          }
          &::-webkit-slider-thumb {
            -webkit-appearance: none;
            height: px2rem(20);
            width: px2rem(20);
            border-radius: 50%;
            background:white;
            box-shadow: 0 px2rem(2) 0 rgba(0, 0, 0, .15);
            border: px2rem(1) solid #ddd;
          }
        }
      }
      .text-wrapper {
        font-size: px2rem(5);
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
  .content-mask {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 100;
    display: flex;
    width: 100%;
    height: 100%;
    background: rgba(51, 51, 51, .8);
  }
}
</style>
