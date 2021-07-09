<template>
  <!-- 请将底层div放置于顶部，<background>除外 -->
  <!-- 他们的故事，从这里开始.... -->
  <xx></xx>  <!-- in the FRANXX -->
<startanime @click="openTheDoor(1)" ref="startanime"></startanime>  <!-- 开屏动画 -->

  <background ref="background"></background>

</template>

<script>

import StartAnimation from "@/components/StartAnimation";
import BackgroundImg from "@/components/BackgroundImg";
import XX from "@/components/XX";

export default {
  name: "main",
  components: {
    startanime: StartAnimation,
    background: BackgroundImg,
    xx: XX
  },
  methods: {
    openTheDoor(flag)  {
      this.$refs.startanime.openTheDoor(flag)
      this.bgimgexpand()
    },
    bgimgexpand() {
      this.$refs.background.bgimgexpand()
    }
  }
}
</script>

<style scoped>

</style>