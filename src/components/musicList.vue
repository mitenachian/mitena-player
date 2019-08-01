<template>
  <div>
    <el-row  v-for="(item, index) in list" :key="index" @click="changeSong(index)">
      <el-col :span="2" :xl="2" :lg="2" :md="4" :sm="4" :xs="24">
        <div class="imgbox" v-if="window.width >=768">>
          <el-image class="coverImg"
           :src="image(item)"
           fit="fill"
           ></el-image>
        </div>
      </el-col>
      <el-col :span="22" :xl="22" :lg="22" :md="20" :sm="20" :xs="24" 
      :class="{ 'musicNow': index === currentIndex }">
        <div class="grid-content bg-purple-light listItem">
          <div class="text">
            <span class="pdlf_10">{{ index + 1 }}</span>
            <el-divider direction="vertical"></el-divider>
            <span ><font-awesome-icon icon="play-circle" /></span>
            <el-divider direction="vertical"></el-divider>
            <span>
              {{ item.title }} / {{ item.artist }}
            </span>
          </div>
          <div class="textRight">
              <el-divider direction="vertical"></el-divider>
              <span ><font-awesome-icon icon="ellipsis-h"/></span>
              <el-divider direction="vertical"></el-divider>
              <span class="pdlf_10 pdrg_10">{{ item.time }}</span>   
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import 'element-ui/lib/theme-chalk/display.css';
import music from '../data/music.js';
export default {
  components: {
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
.el-row {
  margin:10px 0;
}
.clearFix{
    display: block;
    content: "";
    clear: both;
}
.listItem{
  display:  table;
  width:100%;
}
.listItem:hover {
  border: 1px solid #888888;
  border-radius: 4px;
  box-shadow: 7px 7px 7px rgba(0, 0, 0, 0.3);
  cursor: pointer;
}
.listItem .text{
    display:table-cell;
    vertical-align:middle;
    text-align:left;
}
.grid-content {
  border-radius: 4px;
  min-height: 100px;
}
.bg-purple-light {
  background: #e5e9f2;
}
.pdlf_10 {
  padding-left: 10px;
}
.pdrg_10{
  padding-right: 10px;
}
.fontStyleSmall {
  font-size:8px;
  color:#FFA488;
}
.listItem .textRight{
    display:table-cell;
    vertical-align:middle;
    text-align:right;
}
.musicNow {
  border: 1px solid #888888;
  border-radius: 4px;
  box-shadow: 7px 7px 7px rgba(0, 0, 0, 0.3);
}
.imgbox {
  position: relative;
  height: 100px;
  width: 100px;
}
.coverImg {
  position: absolute;
  width: 100%; 
  height: 100%; 
  border-radius:5px;
  left: 0; top: 0;
}

</style>
