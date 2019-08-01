<template>
    <div class="musicPlayerBox">
        <el-row :gutter="10">
            <el-col :xs="24" :sm="24" :md="24" :lg="2" :xl="2"><div>.</div></el-col>
            <el-col :xs="24" :sm="24" :md="24" :lg="6" :xl="4">
                <div v-if="window.width >=1200">
                <musicAlbum/>
                </div>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24" :lg="16" :xl="16">
                <musicTopBox/>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24" :lg="2" :xl="2"><div>.</div></el-col>
        </el-row>
        <el-row :gutter="10">
            <el-col :xs="24" :sm="24" :md="2" :lg="2" :xl="2"><div>.</div></el-col>
            <el-col :xs="24" :sm="24" :md="20" :lg="20" :xl="20">
                <musicList/>
            </el-col>
            <el-col :xs="24" :sm="24" :md="2" :lg="2" :xl="2"><div>.</div></el-col>
        </el-row>
    </div>
</template>

<script>
import musicAlbum from './musicAlbum.vue';
import musicTopBox from './musicTopBox.vue'
import musicList from './musicList.vue'

export default {
  components: {
    musicList,
    musicTopBox,
    musicAlbum,
  },
name: 'home',
data() {
    return {
        window: {
            width: 0,
            height: 0
        }
    };
  },
  created() {
    window.addEventListener('resize', this.handleResize)
    this.handleResize();
  },
  destroyed() {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
