<template>
  <div>
<el-row>
  <el-col :xs="24" :sm="24" :md="6" :lg="6" :xl="6">
    <div class="grid-content bg-purple">
      <musicAlbum/>
    </div>
  </el-col>
  <el-col :xs="24" :sm="24" :md="18" :lg="18" :xl="18">
    <div class="grid-content bg-purple-light">
      <div>
        <span style="color:rgb(255, 208, 75); font-size:30px;margin:10px;line-height: 45px;">Music List</span>
      </div>
      <div class="flex">
        <div class="item" v-for="(item, index) in list" :key="index" @click="changeSong(index)">
          <el-row :class="{ 'musicNow': index === currentIndex }">
            <el-col :span="3" :md="3" :sm="3" :xs="24">
              <el-image v-if="window.width >=768"
              :src="image(item)"
              ></el-image>
            </el-col>
            <el-col :span="17" :md="17" :sm="17" :xs="24">
              <div class="text">
                <span>{{ index + 1 }}</span>
                <el-divider direction="vertical"></el-divider>
                <span ><font-awesome-icon icon="play-circle" /></span>
                <el-divider direction="vertical"></el-divider>
                <span>
                  {{ item.title }} / {{ item.artist }}
                </span>
              </div>
            </el-col>
            <el-col :span="4" :md="4" :sm="4" :xs="24" v-if="window.width >=768">
              <div class="textRight" >

                  <span v-if="index === currentIndex" ><font-awesome-icon icon="music"/></span>
                  <el-divider direction="vertical"></el-divider>
                  <span >{{ item.time }}</span>   
              </div> 
            </el-col>
          </el-row>
        </div>
      </div>
      
       
    </div>
     <div class="clearfix"></div>
  </el-col>
  
</el-row>
  </div>
</template>

<script>
// import music from '../data/music.js';
import musicAlbum from './musicAlbum.vue';
export default {
  components: {
    musicAlbum,
  },
  name: 'musicList',
  data() {
      return {
       window: {
          width: 0,
          height: 0
          },
      };
  },
  computed: {
    currentIndex() {
      return this.$store.state.index;
    },
    list() {
      return this.$store.state.list;
    }
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
  font-size:12px;
}
.item:last-child{
  margin-bottom:  10px;
}
.item:hover {
  color:rgb(255, 208, 75);
}
.el-image {
  height: 60px;
  width: 60px;
}
.musicNow {
  color:rgb(255, 208, 75);
}
.text, .textRight {
   line-height:60px;
   cursor: pointer;
}
</style>
