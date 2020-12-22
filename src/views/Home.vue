<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
  <div id="home">
    <WallContainer></WallContainer>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import WallContainer from "@/components/WallContainer";

export default {
  name: 'Home',
  components: {
    HelloWorld,
    WallContainer
  }
}
</script>
<style>
#home {

}
</style>