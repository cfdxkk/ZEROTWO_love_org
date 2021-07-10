<template>
  <div id="FRANXX">
    <h2>this is FRANXX index</h2>
    <router-link to="/FRANXX/picture">相簿 </router-link>
    <router-link to="/FRANXX/hole">寄语 </router-link>
    <router-view name="FRANXXpicture"></router-view>
    <router-view name="FRANXXhole"></router-view>
    <router-link to="/">返回首页 </router-link>
  </div>

</template>

<script>
export default {
name: "FRANXXindex"
}
</script>

<style scoped>

#FRANXX{
  width: 100vw;
  height: 100vh;

  padding: 0;
  margin: 0;

  position: absolute;
  top: 0;
  left: 0;

  background-color: pink;


}

</style>