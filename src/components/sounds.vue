<template>
  <div id="sounds">
    <audio id="clickaudio">
      <source src="../staticFile/audio/hit_audio.mp3" type="audio/mpeg">
      <!--    Your browser does not support the audio tag.-->
    </audio>

    <audio id="bgaudio">
      <source src="../staticFile/audio/CODE_002.mp3" type="audio/mpeg">
      <!--    Your browser does not support the audio tag.-->
    </audio>
  </div>

</template>

<script>
export default {
  name: "sound",
  methods: {
    clickandplay: () => {

      const clickaudio = document.getElementById("clickaudio")
      clickaudio.volume = 0.05
      clickaudio.play()

      setTimeout(() => {
        const bgaudio = document.getElementById("bgaudio")
        bgaudio.volume = 0.1
        bgaudio.play()
      },500)

    }
  }
}
</script>

<style scoped>

</style>