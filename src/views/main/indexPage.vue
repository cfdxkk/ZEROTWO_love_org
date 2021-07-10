<template>
  <!-- 请将底层div放置于顶部，<background>除外 -->
  <!-- 他们的故事，从这里开始.... -->
  <xx ref="xx"></xx>  <!-- XXXXXXXXXXXXXXXXXXXXX  -->

  <startanime @click="openTheDoor(1)" ref="startanime"></startanime>  <!-- 开屏动画 -->
  <indextopbar ref="indextopbar"></indextopbar>  <!-- 顶部栏 -->

  <!-- 主页背景图 -->
  <background ref="background"></background>

  <!-- 用于存放主页所有用到的音频与音频操作相关脚本 -->
  <sound ref="sound"></sound>




</template>

<script>

import StartAnimation from "@/components/StartAnimation";
import BackgroundImg from "@/components/BackgroundImg";
import XX from "@/components/XX";
import indextopbar from "@/components/indexPage_topbar";

import sound from "@/components/sounds";

export default {
  name: "indexPage",
  components: {
    startanime: StartAnimation,
    background: BackgroundImg,
    xx: XX,
    indextopbar,
    sound
  },
  methods: {
    openTheDoor(flag)  {
      this.$refs.startanime.openTheDoor(flag)  // 渲染开屏动画
      this.bgimgexpand()      //渲染背景图片放大动画
      this.XXattend()         //渲染XX出现的动画
      this.clickAndPlayAudio()       //播放音频，包括开屏动画的点击音效和主BGM
      this.indextopbarAttend()     //渲染indextopbar进入动画
    },
    bgimgexpand() {
      this.$refs.background.bgimgexpand()
    },
    XXattend() {
      this.$refs.xx.XXattend()
    },
    clickAndPlayAudio() {
      this.$refs.sound.clickandplay()
    },
    indextopbarAttend() {
      this.$refs.indextopbar.topbarenter()
    }
  }
}
</script>

<style scoped>

</style>