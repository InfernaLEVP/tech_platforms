<template>
  <!-- <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div> -->
  <router-view/>
  <!-- <img class="world" src="/world.svg" alt=""> -->
</template>

<script>
export default {
    mounted() {
        setTimeout(() => {
            this.$router.push(window.configuratedRoute);
        }, 3000);
    }
}
</script>

<style>
body{
    margin: 0;
    /* background: radial-gradient(ellipse at top, #e66465, transparent),
            radial-gradient(ellipse at bottom, #4d9f0c, transparent); */
    background: url(/main/bg_all.png);
    height: 1920px;
    width: 1080px;
    overflow: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.world{
    position: absolute;
    left: 0;
    top: 400px;
    width: 100%;
    max-width: 100%;
    z-index: -1;
}
*{
    box-sizing: border-box;
}
img{
    max-width: 100%;
}
*{
    outline: none!important;
}
</style>
