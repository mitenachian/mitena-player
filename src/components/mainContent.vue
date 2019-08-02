<template>
  <div>
<el-row>
  <el-col :xs="24" :sm="24" :md="6" :lg="6" :xl="6">
    <div class="grid-content bg-purple">
      <musicAlbum/>
    </div>
  </el-col>
  <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="12">
    <div class="grid-content bg-purple-light">
      <div>
        <span style="color:rgb(255, 208, 75); font-size:30px;margin:10px;;">Music List</span>
      </div>
      <div class="flex">
        <div class="item" v-for="(item, index) in list" :key="index" @click="changeSong(index)">
          <div :class="{ 'musicNow': index === currentIndex }" class="textBox" >
            <div class="imgbox" v-if="window.width >=768">
              <el-image class="coverImg"
              :src="image(item)"
              fit="cover"
              ></el-image>
            </div>
            <div class="text textRight">
              <span>{{ index + 1 }}</span>
              <el-divider direction="vertical"></el-divider>
              <span ><font-awesome-icon icon="play-circle" /></span>
              <el-divider direction="vertical"></el-divider>
              <span>
                {{ item.title }} / {{ item.artist }}
              </span>
            </div>
            <div class="text" >
                <el-divider direction="vertical"></el-divider>
                <span ><font-awesome-icon icon="ellipsis-h"/></span>
                <el-divider direction="vertical"></el-divider>
                <span >{{ item.time }}</span>   
            </div>            
          </div>
        </div>
      </div>
      
       
    </div>
     <div class="clearfix"></div>
  </el-col>
  <el-col :xs="24" :sm="24" :md="6" :lg="6" :xl="6"><div class="grid-content bg-purple"></div></el-col>
</el-row>
  </div>
</template>

<script>
import music from '../data/music.js';
import musicAlbum from './musicAlbum.vue';
export default {
  components: {
    musicAlbum,
  },
  name: 'musicList',
  data() {
      return {
       currentIndex:1,
       list:music,
       window: {
          width: 0,
          height: 0
          },
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
    image(current) {
      return require(`../assets/${current.album}`);
    },
    changeSong(index) {
      this.$store.commit('changeSong', index);
    },
    handleResize() {
      this.window.width = window.innerWidth;
      this.window.height = window.innerHeight;
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background:rgb(255, 208, 75);
  }
  .bg-purple-light {
    background:#545c64;
  }
  .grid-content {
    min-height: 50px;
    height:100%;
  }

.flex {
  display: flex;
  height: auto;
  flex-direction: column;
}

.item {
  flex: 1;
  background-color: #545c64;
  margin:  10px  10px 0 10px;
  justify-content: flex-start;
  color: white;
  font-size: 2em;
}
.item:last-child{
  margin-bottom:  10px;
}
.imgbox {
  height: 60px;
  width: 60px;
  margin-right:10px;
}
.musicNow {
  color:rgb(255, 208, 75);
}
.textBox{
  font-size:14px;
  display:  flex;
  align-content:flex-start;
  
   justify-content:space-between;
  
}
.textBox .text{
  align-self:center;
  align-items: flex-end;
}
.textBox .textRight{
  align-items: flex-start;
}
</style>
