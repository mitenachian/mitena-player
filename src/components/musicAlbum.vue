<template>
  <div class="circle">
    <el-image
      class="imgStyle"
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
  width:100%;
  height:100%;
  border-radius: 5px;
  animation: rotation 15s infinite linear;
}

.circle {
  width:300px;
  height: 300px;
  border-radius:50%;
  overflow: hidden;
  text-align: center;
  
}

@keyframes rotation {
		from {
				transform: rotate(0deg);
		}
		to {
				transform: rotate(359deg);
		}
}
</style>
