<template>
  <div>
    <el-row v-for="(item, index) in list" :key="index" @click="changeSong(index)">
      <el-col :span="2" :md="2" :xs="4">
        <div class="coverImg">
          <el-image
           style="width: 60px; height: 60px"
           :src="image(item)"
           fit="fill"
           ></el-image>
        </div>
      </el-col>
      <el-col :span="22"  :md="22" :xs="20" 
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
      };
  },
  methods: {
    image(current) {
      return require(`../assets/${current.album}`);
    },
    changeSong(index) {
      this.$store.commit('changeSong', index);
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  min-height: 60px;
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
</style>
