<template>
  <div class="imgStyle">
    <el-image
      :src="imgLoad('musicImg01.png')" 
      >
    </el-image>
  </div>
</template>

<script>
export default {
  name: 'musicAlbum',
    data() {
      return {

      }
  },
   methods: {
    imgLoad(current) {
      return require(`../assets/${current}`);
    },
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
