<template>
  <transition name="slide-left">
    <div class="content" >
        <div class="content-wrapper" v-if="isBookProgressAvalable"
        ref="contentWrapper">
          <div class="content-item" v-for="(item, index) in navication.toc" :key="index"
               @click="toPage(item.href)">
            <span class="text">{{item.label}}</span>
          </div>
        </div>
        <div class="empty" v-else>加载中...</div>
    </div>
  </transition>
</template>
<script>
export default {
  name: 'Directory',
  props: {
    isShowContent: Boolean,
    navication: Object,
    isBookProgressAvalable: Boolean
  },
  mounted () {
    // 设置目录的高度
    // const navicationHeight = window.getComputedStyle(this.$refs.contentWrapper).height / 16 - 96
    // document.querySelector('.content-wrapper').style.height = navicationHeight + 'px'
  },
  methods: {
    toPage(href) {
      this.$emit('toPage', href)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/styles/global";

.content {
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  .content-wrapper {
    position: absolute;
    bottom: px2rem(48);
    top: px2rem(48);
    left: 0;
    /*width: 50%;*/
    background: white;
    z-index: 101;
    display: flex;
    flex-direction: column;
    .content-item {
      flex: 1;
      border-bottom: px2rem(1) solid #999;
      margin: 0 px2rem(10);
      display: flex;
      align-items: center;
      .text {
        font-size: px2rem(15);
      }
    }
  }
}

</style>
