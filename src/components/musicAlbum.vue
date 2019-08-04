<template>
  <div class="imgStyle">
    <el-image
      :src="image" 
      >
    </el-image>
  </div>
</template>

<script>
export default {
  name: 'musicAlbum',
  computed: {
    current() {
      return this.$store.getters.current;
    },
    image() {
      return require(`../assets/${this.current.album}`);
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.imgStyle{
  width: 100%;
  height: 100%;
}
.el-image {
    width: 100%;
    height: 100%;
}
</style>
